## SPATIAL DIVERSITY

Code for calculating the spatial diversity of our cities

WEB: [https://pupc.unizar.es/diversidad](https://pupc.unizar.es/diversidad)

CODE: [https://github.com/s-garciap/spatial_diversity](https://github.com/s-garciap/spatial_diversity)

The code uses open libraries for calculating diversity.  
It is based on Python and PostGIS.

### This code calculates the following spatial diversities:
- diversity of age of buildings (continuous variable, standard deviation)
- diversity of building quality (continuous variable, standard deviation)
- diversity of dwelling size (discrete variable, Shanon index and Simpson index)
- diversity of uses (discrete variable, Shanon index and Simpson index)
- other diversities not included in the final version of our maps, but maybe useful in some contexts
    - façade length diversity (continuous variable, standard deviation)
    - number of owners diversity (continuous variable, standard deviation)
    - plot surface diversity (continuous variable, standard deviation)
    - residential floor area ratio diversity (continuous variable, standard deviation)

### Required installation:
- Python environment with the libraries:
  - `pandas`
  - `geopandas`
  - `sqlite3`
  - `sqlalchemy`
  - `psycopg2`
  - `time`
  - `os`
- `sgp_utils` available at: https://github.com/s-garciap/sgp_utils/blob/main/sgp_utils.py (this module mainly facilitates working with POSTGIS and SPATIALITE EXTENSION)
- Have PostgreSQL with the PostGIS extension installed on your computer

### Required files:
The methodology is designed to work with cadastral cartography from the Spanish General Directorate of Cadastre. Numerous academic articles have explained the peculiarities and possibilities in the way the Spanish Cadastre shares information. We highlight this reference: 'Mora-García, R T, M F Céspedes-López, J C Pérez-Sánchez, and V R Pérez-Sánchez. 2015. “Reutilización de datos catastrales para estudios urbanos”. In Análisis espacial y representación geográfica: innovación y aplicación, editado por J de la Riva, P Ibarra, R Montorio, and M Rodrigues, 295–304. Universidad de Zaragoza - AGE.' ([link](https://congresoage.unizar.es/eBook/trabajos/031_Mora-Garcia.pdf))
  
The preparatory cadastral information tables needed are detailed below:

- Cadastral general data in a PostgreSQL database, with polygon geometry. The table should be named `par_g_{city}` and incorporate the following columns:
  - `refact` : cadatastral reference (id)
  - `scons` : floor area ratio
  - `v_c` : number of dwellings / residential units
  - `v_sum`: residential floor area ratio
  - `scub_n`: roof surface
  - `sparc_n`: plot surface
  - `nprop`: number of propietaries
  - `edad_bi`: age of construction
  - `consq_avgp`: average quality of each catastral unit
  - `i_sum`: industrial floor area ratio
  - `o_sum`: officies floor area ratio
  - `y_ter_sum`: health and charity (tertiary) floor area ratio
  - `c_sum`: commercial floor area ratio
  - `g_sum`: Leisure and Hospitality floor area ratio
  - `t_sum`: Shows and Theaters floor area ratio
  - `k_sum`: Sports floor area ratio
  - `y_eq_sum`: Health and Hospitality (facilities) floor area ratio
  - `e_sum`: cultural floor area ratio
  - `r_sum`: religius floor area ratio
- Detailed record of each of the premises or cadastral units that are part of a plot. The table should be named `r14_{city}` and incorporate the following columns:
  - `refcat`: cadatastral reference (id)
  - `cuso`: use code for each cadastral unit ('V' = residential)
  - `stotal`: floor area ratio of cadastral unit
- Façade line. The table should be named `par_g_fline_{city}` and incorporate the following columns:
  - `refcat`cadatastral reference (id)
  - `lfachada`: façade length (building line in contact with plot geometry)
  
### Code contributor:
Sergio García-Pérez
sgarciap@unizar.es
