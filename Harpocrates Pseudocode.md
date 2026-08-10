Weka Detection Engine -> 

*NOTE WEKA is outdated and the actual implementation will use DL4J or Smile for optimization. WEKA provides a v1 implementation without all the complexities that come with newer models and is this used for pseudocode purposes*

*data should be clustered depending on if the instances are similar -> threat detection data types should be clustered separately - network detection threats are clustered into network threats so on and so forth* 

 
```JAVA PSEUDOCODE FOR DETECTIONENGINE CLASS
IMPORT weka Classifers FROM classifiers //import all weka libraries
IMPORT weka RandomForest FROM classifiers 
IMPORT weka Instance FROM core 
IMPORT weka Instances FROM core 
IMPORT weka DataSource FROM converters

CREATE class DetectionEngine THEN //detection engine class 
INSTANTIZE Instances class from classifiers 
INSTANTIZE RandomForest model from classifiers THEN 
LOAD dataset //must be instantized to be used in loadData function 

CREATE function loadData PARSING filePath THROW EXCEPTION THEN //weka Instances
IF filePath DOESN'T EXIST THEN //if the dataset file doesn't exist 
THROW FileNotFoundException


INITIALIZE DataSource source AS new DataSource PARSING filePath //data is gathered from the filePath 
INITIALIZE data AS getData FROM source  //data is extracted from the data source 

IF Index from data EQ -1 //if the class index is not found in the dataset
THEN SET Index PARSING numattributes from data MINUS 1 //set the class index to the last index. numattributes counts all variables 
RETURN data //data is passed back to the function as Instances class data type 

END FUNCTION

CREATE function trainingModel PARSING trainingFile THROW EXCEPTION THEN //train weka ML 
CREATE variable trainingData EQ loadData PARSING trainingFile (Path) //training data uses trainingFile and loads the data 
SET model AS RandomForest //RandomForest class becomes the model variable 

model FUNCTION set tree number (x)
model FUNCTION buildClassifier(trainingData)
PRINT OUT successful training WITH trainingData 

//here we need to classify an instance from the dataset 
CREATE function classifyInstance PARSE dataFile and instanceIndex THROW EXCEPTION THEN //we need to take the loaddata function and then rin the source we want data to be extracted from 
INITIALIZE dataSet AS loadData PARSE dataFile DATA TYPE Instances //the dataset is the data from the loaded data source 

//then we need to bomb proof the index function by checking if the index exists 
IF instanceIndex LQ 0 OR instanceIndex GEQ totalInstances from dataSet THEN
THROW IndexOutOfBounds Exception 

/*the lines of pseudocode following aim to, firstly, pull an event out of the dataset initializing the instance of the instance index. secondly, the classifyInstance of the selected instance that is selected runs the trained model and returns a double, which is the index value of the class attribute list of possible values {benign, malicious, conspicuous} will all return 0.0, 1.0 or 2.0 which varies on model depiction. Weka's universal internal type is a double data type. Lastly, predictionIndex needs to have the attribute object from the class column from the dataSet and to look at which string label corresponds to the predictedIndex and returns that value. The double needs to be casted to an int so that value() can expect an int index to traverse the list. instanceIndex will return a String value from the list and int is out lookup key */ 

INITIALIZE instance AS dataSet FUNCTION instance PARSE instanceIndex 
INITIALIZE predictionIndex AS model FUNCTION classifyInstance PARSE instance 
RETURN dataSet FUNCTION classAttribute FUNCTION value CASTED TO int PARSING predictionIndex 

END FUNCTION

CREATE main function 

CREATE try block
INITIALIZE DetectionEngine object 

//paths towards dataset source files
INITIALIZE trainingPath AS "data/x/x" 
INITIALIZE filePath AS "data/x/x" 
INITIALIZE index AS 0 

TRAIN MODEL WITH trainingPath 

//classify instance 
INITIALIZE result AS classifyInstance PARSING filePath and index 
PRINT predicted class AND result 

CATCH exception AND PRINT stacktrace() 


``` 

*Overall Functionality Summarized*:
Weka DataSource loads .arff or .csv files and sets the final attribute as the class label 

RandomForest detects classification tasks and is a model training technique 

Test data is loaded and predicts the class of the provided instance 

Missing files, invalid indexes and data formatting issues are handled 


Potentially switch to BufferedReader on source files to read byte streams 

.arff example:

```
@relation threat_detection

@attribute packet_size numeric

@attribute duration numeric 

@attribute protocol {tcp, udp, icmp}

@attribute threat {malicious, benign}

@data 
500,0.2,TCP,benign
1500,1.5,UDP,malicious
```
