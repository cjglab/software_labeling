# Software Architecture Decomposition
This repository contains supplementary material and data related to the papaer about Software Architecture Decomposition under revision


Content of the root directory
-----------------------------

app_experiments_spl.py
        : main application used to apply the analysis protocols to the SPL proprietary software's graph and
        to collect results and data for plots

app_experiments_syntetic_swap.py
        : main application used to generate synthetic graphs to apply the analysis protocols and
        to collect results and data for plots

experiments.py
        : module used by the two main applications, that implements the loops used to select the nodes using the 
            protocols, apply the label propagation algorithm and collect the statistics

loggingx.py
        : module containing a simple extension to the standard Python logging system, based on Log4j, 
        used by experiments.py module

requirements.txt
        : configuration file, to use with pip, containing the list of external libraries used by the applications

[netx]
        : module extending NetworkX library, used by experiments.py module


Content of [data] directory
---------------------------

This directory contains the datasets used in the experiments.

4c00c2ca-component-graph-1-r00-vertices.csv, 4c00c2ca-component-graph-1-r00-edges.csv
        : Graph representation of the proprietary software used for the experiments on real data 
        
spl-results.csv
        : Results collected from the experiments, using different protocols, carried out on the proprietary software

jdeps-2.8.0.odem
        : Object Dependency Exploration Model (ODEM) file describing the structure of CDA software.
            It contains 21 isolated nodes, 4 connected components with 2 nodes, 1 connected component with 3 nodes,
            a connected component with only 5 nodes, and the largest connected component composed by 1213 nodes and 
            5692 edges.

jdeps-2.8.0-connected.odem
        : As 'jdeps-2.8.0.odem' but containing only the largest connected component (1213 nodes, 5692 edges).

jdeps-categories-all.csv
        : One-to-one map used to convert Java namespaces into abbreviated names

jdeps-categories-c7.csv
        : Map representing the grouping of Java namespaces into 7 different categories

[experiments]
        : This empty directory is necessarily created, for containing the csv result files when launching the 
            experiments

File formats
------------

The following section describes the structure of the files used in the experiments

*-vertices.csv and *-edges.csv
        : simple format used to serialize a graph, based on two CSV files.
            The file '*-vertices.csv' has at least the column 'id' containinga unique id for each node.
            All other columns are used as extra attributes.

        : For the experiments, the other important column is 'category', containing the node's classification.

        : The file '*-edges.csv' contains at least two columns: the edge source and target.
            The column names are used to specify whether the graph is directed ('source', 'target')
            or undirected ('id1', 'id2').
            All other columns are used as extra attributes.

*.odem
        : ODEM file is a simple XML file, generated by CDA when the application's dependency
            graph is exported.

*-categories-*.csv
        : It is a simple map 'category->Java namespace'. The column 'count' is not used
        (it is the number of classes inside the namespace).

spl-results.csv
        : It contains the results of the experiments applied to the real dataset. It is composed by
            36 columns

- **mode** : protocol used (**rand**, **layer**, ...)
- **k** : number of labels selected in each category, as integer (absolute value) or quota in the range (0,...1)
- **algorithm **: algorithm used to propagate all labels
- **acc** : classification mean accuracy
- **acc_sdev** : classification accuracy standard deviation
- **n_labels[b] ... n_labels[g]** : effective (integer) number of labels assigned to each category
- **n_labels** : total number of labels used as seeding labels
- **b.b ... g.g** : confusion matrix organized linearly where the column name is **actual** x **predicetd**


