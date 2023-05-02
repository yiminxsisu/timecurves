# How to run the existing code on MacOS

## (optional) step 1: generate curve files
note: I met a `java.lang.NoClassDefFoundError: cern/colt/matrix/DoubleMatrix2D` error when running this on my Mac (M1), but the bug disappears in a Linux environment.

1. install java: https://www.java.com/en/download/ 
2. make an output directory, e.g., `mkdir test-output`
3. go to the server folder: `cd server`
4. run `java -jar foldSimilarityMatrix.jar ../test-data ../test-output`
5. copy curve files to the client directory: `cp ../test-output/0226-T3_curves.curve ../client/timecurves/example-session`


## step 2: display the visualization
1. install php: `brew install php` 
2. make sure php is installed: `php -v`
2. go to the client folder: `cd client`
3. start the php server: `php -S localhost:8080`
4. go to [localhost:8080](http://localhost:8080/) and you should be able to see the curve visualization

*************************************************


# Time curves

Time curves are a visualization for temporal data, explained in detail here: www.aviz.fr/~bbach/timecurves. 

The code for time curves is divided into a client and a server. The client front end is written in java scrpt and relies on d3. The backend, is written in Java and calculates the curves which are then visualized by the client side. Those files have the extension curve and are in json format. 

Currently, the repo contains the client side. The server side calculating curves for wikipedia articles, videos, and dynamic networks comes soon. 


## Client Code

The client code constist of an index.php, which is a PHP in order to track sessions. Curve files are loaded from a directory called timecurves. 

While index.php sets up the visualization context, the core file is called 'curvepile.js'. 

Curvepile.js corresponds to an svg that can display multiple curves and make individial curves visible or hide them. 


## Server Code

The server code imports similarity matrices, as indidated on the website: www.aviz.fr/~bbach/timecurves. 
The compiled version (foldSimilarityMatrix.jar) takes two commandline parameters: input and output folder: 

'java -jar foldSimilarityMatrix.jar myInputDir myOutputDir'

This command translates all similarity matrices in 'myInputDir' into .curve' files in the 'myOutputDir'. 

The class that loads the matrices in '.json' format is 'fr.inria.aviz.progresio.server.matrixImport.DistanceMatrixImporter.java'. 


