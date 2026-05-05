---
excalidraw-plugin: parsed
tags:
  - excalidraw
cssclasses:
  - daily
  - reflection
---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠== You can decompress Drawing data with the command palette: 'Decompress current Excalidraw file'. For more info check in plugin settings under 'Saving'

# Big Data
After the [[_ Visualization _|Visualization]], [[OwnerFirstName OwnerLastName|Ori-Sama]] will learn about the big data:

- [[Map Reduce Fundamentals]]
- [[Hadoop Components]]
- [[HDFS]]
- [[Data Replication Principles]]
- [[Setup Hadoop]]
	- [[IBM]]
	- [[Cloudera]]
	- [[HortonWorks]]
	- [[Name and Data Nodes]]
	- [[Job]] & [[Task Tracker]]
	- [[MIR Programming]]
	- [[Sqoop]]:
		- [[Loading Data in HDFS]]
	- [[Flume]], [[Scribe]] :
		- [[Unstructured Data]]
	- [[SQL]] with [[Pig]]
	- [[DWH]] with [[Hive]]
	- [[Scribe]], [[Chukwa]]:
		- [[Weblog]]
	- [[Mahout]]
	- [[Zookeeper]] [[Avro]]
	- [[Storm]]:
		- [[Hadoop Realtime]]
	- [[Rhadoop]], [[RHIPE]]
	- [[rmr]]
	- [[Cassandra]]
	- [[MongoDB]], [[Neo4j]]

Next stop: [[_ Data Ingestion _|Data Ingestion]]…



## 1. Caractéristiques générales du [[_ Big Data _|big data]]

- **Définition** : ensemble des technologies et méthodologies permettant le traitement, le stockage et l’analyse de très grandes masses de données, souvent hétérogènes et produites à grande vitesse.
    
- **Origine** : explosion des données issues du web, des réseaux sociaux, de l’[[IoT]], du e-commerce et des systèmes transactionnels.
    
- **Objectif** : extraire de la valeur (décisionnel, analytique, prédictif) à partir de données massives et complexes.
    

---

## 2. Les axes fondamentaux du [[_ Big Data _|big data]]

### A. Les “5V” du [[_ Big Data _|big data]]

1. **Volume** : taille massive des données (exabytes, zettabytes).
    
2. **Vélocité** : flux de données en temps réel (streaming).
    
3. **Variété** : diversité des formats (structurés, semi-structurés, non structurés).
    
4. **Véracité** : fiabilité et qualité variable des données.
    
5. **Valeur** : finalité analytique et décisionnelle.
    

---

### B. Typologie des données

- **Structurées** : bases relationnelles ([[SQL]]).
    
- **Semi-structurées** : [[JSON]], [[XML]], logs.
    
- **Non structurées** : texte libre, images, vidéos, sons, [[réseaux sociaux]].
    

---

### C. Architecture et écosystème du [[_ Big Data _|big data]]

1. **Stockage distribué**
    
    - Hadoop Distributed File System ([[HDFS]]).
        
    - Systèmes [[01 - Learning/Raw assets/noSQL]] ([[MongoDB]], [[Cassandra]], [[HBase]]).
        
    - Data lakes (S3, [[Azure Data Lake]]).
        
2. **Traitement distribué**
    
    - [[Hadoop]] [[MapReduce]] (lot/batch).
        
    - [[Apache]] [[Spark]] (mémoire, batch et streaming).
        
    - [[Apache]] Flink, [[Storm]] (stream processing).
        
3. **Ingestion et flux de données**
    
    - [[Apache]] [[Kafka]], [[Flume]], [[Sqoop]].
        
4. **Analyse et [[ML|machine learning]]**
    
    - [[MLlib]] ([[Spark]]), [[Mahout]], [[TensorFlow]], [[Scikit-learn]].
        
5. **Visualisation et décisionnel**
    
    - Tableau, [[Power BI]], [[Kibana]].
        

---

### D. Principes fondamentaux

- **Parallélisation et distribution** des traitements.
    
- **Tolérance aux pannes** : réplication des données et redondance.
    
- **Scalabilité horizontale** : ajout de machines au [[cluster]].
    
- **Approches hybrides** : intégration [[SQL]]/[[01 - Learning/Raw assets/noSQL]], [[cloud computing]].
    

---

### E. Modèles et paradigmes

- **Batch processing** : traitement par lots ([[Hadoop]] [[MapReduce]], [[Spark]] batch).
    
- **Stream processing** : traitement en temps réel ([[Kafka]] + [[Spark]] Streaming, [[Flink]]).
    
- **[[Lambda architecture]]** : combinaison du batch et du stream.
    
- **[[Kappa architecture]]** : simplification, uniquement stream.
    

---

## 3. Points essentiels pour un concours académique

- **Maîtrise du paradigme distribué** ([[MapReduce]], [[Spark]]).
    
- **Compréhension du rôle de l’écosystème [[Hadoop]]**.
    
- **Lien avec les bases [[01 - Learning/Raw assets/noSQL]]** comme support de stockage.
    
- **Connaissance des modèles analytiques** : descriptive, prédictive, prescriptive.
    
- **Évolution vers le cloud** : [[AWS EMR]], Google [[BigQuery]], [[Azure]] Synapse.
    
- **Défis actuels** :
    
    - Gouvernance et qualité des données.
        
    - Protection des données personnelles (RGPD).
        
    - Optimisation énergétique (green computing).
        

# Excalidraw Data

## Text Elements
%%
## Drawing
```compressed-json
N4KAkARALgngDgUwgLgAQQQDwMYEMA2AlgCYBOuA7hADTgQBuCpAzoQPYB2KqATLZMzYBXUtiRoIACyhQ4zZAHoFAc0JRJQgEYA6bGwC2CgF7N6hbEcK4OCtptbErHALRY8RMpWdx8Q1TdIEfARcZgRmBShcZQUebQAObQBmGjoghH0EDihmbgBtcDBQMBKIEm4ICgArAGs2AEkATQBlZQBZYgA5ACUAdgBxbuxiAAYATgA1XtSSyFhECsDsKI5l

YJnSzG5nJJGR/lKYbZ4AVjHtHnjek8uxsYBGADY7vkLIChJ1biT7xIAWPYjHh/P73AGPU4HSCSBCEZTSbi/R7aAF7YGg8GQt4QaxrcSofbY5hQUhsGoIADCbHwbFIFQAxPcEEymRtIJpcNgaspSUIOMQqTS6RISdZmHBcIFsmyIAAzQj4fDNWDrCSCDwy4mk8kAdU+km4r1mEC1ZIQypgqvQ6vKUIgvPhHHCuTQ9ztbAl2DUR1deztPOEcHqxBdq

DyAF07bLyJlg9wOEJFXbCPysBVcCMZbz+U7mKHisb5vikm8AL52sIIYiIkEAk4neIjN3YxgsdhcNA/O2t1icTqcMSIy71pJjH5jZPMAAi6SgVe4soIYTtmmE/IAosFMtlQwmk9ihHBiLg59XXdcTvd7r1Tjeko87UQODV44n8I+2Fz52hF/gwoVS3ASM6FwOA4GVE98QLaAYUyCpj1IF8DgYQgEAoAAhTluWzAVqVpBlZUIoiNggbARClKB6jnfR

lW1Sk8OFdBGWZFiSLI0gKKojJMK5AM+VwoUKlFDhxUlLIoDY8jxK4/QADEFSVFV8RNalbUKUipOyGTaLNPViC+NAjUgdjOOonTyQtK0VI1ZCTOk6jumER1nURWzNMo6iAHlPW9RE/XUuytOo2TOCgWTcH0BUfVQE43I4+yMhC7JmkIIx8R4QlSkCjyMgAFSwKAAEEiGUDt0GCWUJLi0yMgg0gio4tgKBhXAz1QPd3wC9yZPXflCsa5qQjanEBsk+

KgoyfrSQoXL4GUnCSOYbBSUVAANbhriSbRYvUpaVvwRpuEvOJenuU50TBEYIR20ojDYAxuALSB6AIIR8XuADqoS/RHP43NQ3tNdq2QnkSBStLDUyyBQeIZUEDgI6QdIEg2jYYgEF63BNGCNrf2XdSYcFfC0CeiB0OpYbSGUDkAAoeGvaheAZpnekZkZtoAShlboEGURNJUWancDp3ZGZ4UXeAl9mTi5z6uvGqBzIQbyoHbXc32Q6MIoQHnU2R1ZH

uxLIsZx7gSTeu1sCIBG0HNhA7Q4bWzdIC3sWEKAn3xO25dKOwqgQZZmGaR24FR9HMex79UDx+31M5VXGFy+78ENws5oqMJgmWdsZTI4kDFmhY0A6j8v1xpdY+NfBQiK7PE+T19FQA8ByzoeVgnzQDSyAA===
```
%%