# Document technique – Label Studio


## 1 – installation et démarrage de l’application

### installation par docker
Executer la commande suivant dans Docker
```
docker run -it -p 8080:8080 -v labelstudio-data:/label-studio/data heartexlabs/label-studio:latest
```
puis se rendre sur navigateur a l'adresse ```http://localhost:8080/``` et se connecter

### installation par pip
```
# Requires Python >=3.8
pip install label-studio

# Start the server at http://localhost:8080
label-studio
```

## 2 – création d’un projet
Dans label studio, en haut à droite, « Create » pour créer un projet.
3 onglets s’ouvrent à nous

### 2.1) 1er onglet : Project Name
On renseigne juste de quoi différencier notre projet des autres : un nom et une description

### 2.2) 2eme onglet : Data Import
Le fichier contenant les informations des PDF sera un fichier JSON organisé comme l'exemple fourni ```exemple.json```
 
Lors de l’importation, cocher “treat csv/tsv as LIST OF TASKS”.
Noter qu’il est possible d’importer d’autres fichiers par la suite si on veut rajouter des documents plus tard.

### 2.3) 3eme onglet : Labelling Setup
Beaucoup de templates s’affichent, mais on va choisir « custom template » en bas a gauche. Puis, copier-coller le code suivant :
```
<View style="display: flex; gap: 32px; height: 800px;">

   <!-- Left Column: Scrollable Document Viewer Only -->
   <View style="flex: 1; overflow-y: auto; border: 1px solid #ccc;
padding: 8px;">
     <Text name="doc" value="$text" />
   </View>

   <!-- Right Column: Relevant Section + Questions -->
   <View style="flex: 1; overflow-y: auto; border: 1px solid #ccc;
padding: 8px;">
     <Header value="🔹 Step 1: Select the section of interest from the
document."/>
     <Labels name="section" toName="doc" choice="single">
       <Label value="Relevant Section" background="#FFD700"/>
     </Labels>

     <Header value="🔹 Step 2: Answer the following questions by
selecting text spans."/>

     <Header value="Q1: What is the v1 value?"/>
     <Labels name="v1" toName="doc" choice="single">
       <Label value="v1" background="#FFB6C1"/>
     </Labels>

     <Header value="Q2: What is the v2 value?"/>
     <Labels name="v2" toName="doc" choice="single">
       <Label value="v2" background="#ADD8E6"/>
     </Labels>

     <Header value="Q3: What is the v3 value?"/>
     <Labels name="v3" toName="doc" choice="single">
       <Label value="v3" background="#90EE90"/>
     </Labels>

     <Header value="Q4: What is the v4 value?"/>
     <Labels name="v4" toName="doc" choice="single">
       <Label value="v4" background="#FFD700"/>
     </Labels>

     <Header value="Q5: What is the v5 value?"/>
     <Labels name="v5" toName="doc" choice="single">
       <Label value="v5" background="#FFA07A"/>
     </Labels>

     <Header value="Q6: What is the v6 value?"/>
     <Labels name="v6" toName="doc" choice="single">
       <Label value="v6" background="#DA70D6"/>
     </Labels>

     <Header value="Q7: What is the v7 value?"/>
     <Labels name="v7" toName="doc" choice="single">
       <Label value="v7" background="#87CEEB"/>
     </Labels>

     <Header value="Q8: What is the v8 value?"/>
     <Labels name="v8" toName="doc" choice="single">
       <Label value="v8" background="#FF8C00"/>
     </Labels>
   </View>

</View>
```

Ce template est modifiable, ici, les indicateurs sont au nombre de 8 et nommés de V1 a V8, on peut en ajouter, en supprimer, ou changer leur nom et couleur en fonction de ce qu’on cherche.
Exemple : on cherche la valeur du Cmax
```
<Header value="Question : What is the Cmax value?"/>
     	<Labels name="Cmax" toName="doc" choice="single">
       	<Label value="Cmax" background="#87CEEB"/>
     	</Labels>
```
		
		
## 3 – Annotation
 
Une vue d’ensemble est proposée, avec chaque entrée correspondante à un document, on peut cliquer sur le document que l’on souhaite annoter.
 
Une fois le document sélectionné, indiquer la section à étudier (label « Relevent Section », en jaune) puis, mettre les labels sur les valeurs à l’intérieur de la section définie. Une fois les labels appliqués, cliquer sur « Submit ».
Une fois que tous les documents sont annotés, il est temps d’exporter.

## 4 – Exportation
 
Une fois l’annotation terminée, il faut exporter les données.
Au format JSON, cela se structure exactement comme l'exemple initial
