*** Aquest repositori conté el codi complet de l'elaboració del métode Random Forest Revisited. ***
---
El propòsit d'aquest codi és l'elaboració d'un mètode basat en Random Forest que sigui capaç de gestionar valors nuls internament, sense imputacions.

*** CONTINGUT *** 
---
El repositori conté 2 arxius amb el mateix continut anomentas RandomForestRevisited i un per una prova ràpida
1. Un arxiu per Python (RandomForestRevisited.py)
2. Un arxiu per obrir com un notebook a Jupyter o Colab (RandomForestRevisited.ipynb)
3. Un arxiu per una prova ràpida, amb el dataset Mammographic Mass, llest per executar directament (RFRtest.ipynb)

*** INSTALACIÓ ***
---
Per executar el codi hi ha diverses opcions;

A. Amb l'arxiu notebook (.ipynb, MILLOR OPCIÓ)
   1. Descarregar fitxer: Click als 3 punts, download
   2. Pujar fitxer a google drive o obrir-ho driectament en local si es disposa de Jupyter Lab o Jupyter Notebook
   3. Obrir Google Colab al navegador y seleccionar l'arxiu pujat

B. Amb un IDE local 
    1. Descarregar l'arxiu .py o clonar amb git: git clone https://github.com/Isaacmel5/Random-Forest-Revisited.git
    2. Instalar dependencies, ja que el codi esta pensat per colab(!pip command)
    comandes: pip install ucimlrepo pandas numpy scikit-learn graphviz xgboost lightgbm
    3. Obrir arxiu i executar

*** MANUAL ***
--
Per exectar el codi, s'han d'anar executant les celes en ordre, seguint les seccións que hi ha:
Llibreries(8), Decision Tree(1), Random Forest(1), Functions(4), Datasets(6), Analisi del dataset(13), Main test(3), Dataset Imputation amb filllna()(1), 
cross validations(1), XGBoost test(1) i ligthGBM test(1).

PER UNA PROVA RAPIDA USAR L'ARXIU: RFRtest.ipynb 
---
<<< Instruccions per el codi complet: RandomForestRevisited.ipynb >>
---
Es poden excutar fins a Functions sense tocar res, pero a DATASETS cal escollir un dels usats i executar aquest només.
ANALISIS DEL DATASET: IMPORTANT
    - En aquest punt cal tenir en compte que hi ha un dataset ( Myocardial Infarction Complications) que és       Multilabel. Per tant per aquest dataset cal seleccionar un target dels 12, "ZSN" és el target binari usat.   
    - Quan es busca info. d'un target cal posar el nom exacte, per exemple a: print(ydata["class"].unique())         #Mirar posibles valors del target
      cal mirar que el nom del target sigui identic al obtingut a : #Posibles targets print(ydata_full.head())
    - També tenir en compte que si no és multilabel cal fer ydata = ydata_full #Si nomes hi ha un target
    - Si és Myocardial Infarction (muiltilabel), executar la cela previa.
    - El codi de Oversampling/undersampling NO s'ha d'executar, és per copiar al Main Test si es vol.
    
MAIN TEST: 
    - Aqui es pot afagir el sampling si es vol, tenir en compte posar el nom de x_oversampled/undersampled en comptes de x_train i el mateix per y_train
    - Utilitzar els valors donats abans per optimal_params per provar parametres raonables i amb sentit en: rf_custom = RandomForest(n_trees=25, max_depth=5, max_features=2).
    
ALTRES TEST:
    - Tenir en compte els comentaris de guia dins el codi

*** Dades Sintetiques ***
---
Per provar dades sintètiques de diferents tipus, es pot usar un petit codi per generar valors aleatoris pero controlats, tal i com es va fer durant el treball.
Pots afegir aquest codi al MAIN TEST. Just despres dels imports i abans de : # Substitueix valors especials per NaN
Xdata.replace(['?', -1, 'unknown', 'Unknown', ''], np.nan, inplace=True).

Codi d'exemple per provar dades sintètiques:

```python
from random import choices
# 1. Definir grandària
n = 100

# 2. Crear columnes numèriques enters i reals
ints   = np.random.randint(0, 10, size=n)
floats = np.random.randn(n) * 5 + 2

# 3. Crear columna categòrica (dtype 'category')
cats = pd.Categorical(choices(['A','B','C'], k=n))

# 4. Crear columna de strings lliures
strs = np.array(choices(['foo','bar','baz','qux'], k=n), dtype=object)

# 5. Afegir NaN a l’atzar
floats[np.random.choice(n, size=20, replace=False)] = np.nan
strs  [np.random.choice(n, size=10, replace=False)] = None

# 6. Construeix el DataFrame
X_synth = pd.DataFrame({
    'enter': ints,
    'real': floats,
    'cat': cats,
    'text': strs
})

# 7. Crea un target binari 
y_synth = pd.Series(choices([0, 1], k=n), name='target')

Xdata = X_synth
ydata = y_synth

