---
name: Network Analysis
topic: NetworkAnalysis
maintainer: Fabio Ashtar Telarico (@FATelarico), Pavel N. Krivitsky (@krivit)
email: Fabio-Ashtar.Telarico@fdv.uni-lj.si
version: 2023-05-08
source: https://github.com/FATelarico/ctv-network
---

This CRAN Task View contains a list of packages that can be used for dealing with networks (also known as _relational data_ and _graphs_).

This list of R packages is curated to include tools specifically designed for analysing and modeling relational data. These packages facilitate the examination of phenomena - be they natural, social, or otherwise artificial - that manifest themselves in the relations between one or more sets of entitiess.
Conversely, the list excludes packages that primarily deal with graphical models defined as graph representions of conditional in/dependence between variables. This includes Markovian graphs, which, despite their relevance in statistical modeling, are better covered under the CRAN TaskView on [Graphical Models](https://cran.r-project.org/web/views/GraphicalModels.html). This distinction keeps the list focused on network analysis that goes beyond mere statistical dependencies, aiming instead to explore broader relational dynamics.

This page is articulated in sections listing the packages/functions to perform specific operations on networks. The packages are categorised based on their scope and focus as follows:

1. The first section provides a review of all-in-one R packages for basic network-analytic operations such as creating, manipulating, and describing relational data.

2. Subsequently, packages offering models and inference tools applicable across disciplines and fields of interests are discussed. Here, a distinction is drawn between frequentist and Bayesian methods. 

2. Then, the focus shifts to packages containing data structures, methods, and model with a narrower field of application. The list includes some of the areas where network methods are more widely applied: ecology, bibliometrics, (bio)-chemistry, neurosciences and psychology, public health, the social sciences and economics.

4. Finally, packages and functions for two advanced network-analytic tasks are presented: visualisation and clustering. In the latter case, the items listed are distinguished on the basis of their approach into three categories:

    - community detection,
    - blockmodeling;
    - others.

Some packages could be placed under more heading because they can perform multiple tasks (e.g., clustering and visualisation). But for the sake of brevity, non-core packages are listed only once: in the section that described each package's main use case.

If you think that some package is missing from the list, please file an issue in the GitHub repository or contact the maintainer.

# Main Packages & Basic tasks

- `r pkg("igraph", priority = "core")` provides tools for creating, manipulating, and analysing network structures with a focus on _nice_ graphical representations and fast algorithms to operate on large datasets (particularly manipulating data and dealing with vertex attributes).

  - *Approach*: igraph takes a somewhat 'basic' approach to network analysis. However, it still contains a lot of functionality, including
calculating network properties, generating random graphs for simulations, etc. and will probably fit most users' needs.

  - *Flexibility*: any of the functions  are provided in two versions: for direct assignment and a 'piped' version $\big($e.g., `igraph::E(net)$attribute <- x` vs `net <- igraph::set_edge_attr(net, 'attribute', value = x)`$\big)$.
  
  - *Support*: There are tons of online resources answering virtually any question concerning _how_ to do anything in `igraph` thanks to a large  community and active maintainers.
  
  - *Extensions*: There are a number of add-on packages that integrate igraph with `Shiny`, `r pkg("ggplot2")` and other drawing tools, or provide sample datasets. According to the latest review,^[see: Kanevsky, Gregory. 2016. 'R Graph Objects: igraph vs. network. _R Bloggers_. January 30, 2016.  https://www.r-bloggers.com/2016/01/r-graph-objects-igraph-vs-network/] `igraph` has many more extension that the closest runner-up, `network`/`statnet`.

- `r pkg("statnet", priority = "core")`  is a collection of packages (incl. `r pkg("network, priority = "core"`) developed by the _statnet_ team at the
University of Washington.

  - *Approach*: It is not always user-friendly because its focus is on statistically testing models based on  Exponential-Family Random Graph Models (ERGMs) and other modeling tools;
 
  - *Flexibility*: New users may find it useful to install only the two basic packages in `statnet`: `nework` and `sna`. Note that, as `igraph`, also these packages suit both traditional coding and a 'piped' approach; 
 
  - *Comprehensiveness*: `statnet`'s (and `network`'s/`sna`'s) biggest advantage is that it allows users to carry out most network-analytical operations, especially in dealing with social network analysis (SNA). But the trade-off, of course, is that the amount of possibilities makes life harder for new users.

- `r pkg("graph")` is a package available on [Biocondutor](https://bioconductor.org/packages/release/bioc/html/graph.html) designed for handling graph-based data structures and performing basic operations on them. It provides a simple and intuitive interface for constructing, manipulating, and analysing graphs.^[Since this Task View focuses on `R` packages available on CRAN, `graph` is not covered as extensively as its main competitors.]

  - *Simplicity*: `graph` focuses on providing fundamental functionalities for graph-based tasks, such as graph construction, visualization, and basic analysis. So, it does not offer the same level of statistical modeling capabilities as `statnet` and is less geared towards large networks than `igraph`.
  
  - *Documentation*: `graph` benefits from a clear and concise documentation, making it accessible to users of all levels. Additionally, it offers straightforward tutorials and examples to help users get started with graph analysis in R.
  
  - *Extentions*: `graph` can be expanded with other packages containing efficient algorithms (for tasks such as shortest path, connectivity etc) and different layout algorithms.

- `r pkg("intergraph, priority = "core")` is not a network analysis package _per se_. Rather it allows to easily convert objects produced by `statnet` packages into `igraph`s (or a data frame) and vice versa. Thus, it is a must-have utility for leveraging multiple packages' functionalities and ensuring compatibility between several users' workflows.

## Network Construction

Altough the two core packages for network analysis in `R` can create a wide range of networks from different types of inputs, there are also specialsied packages for narrower fields of application.

  - `r pkg("BoolNet")` provides tools for assembling, analysing and visualising synchronous and asynchronous (probabilistic) Boolean networks as well as  Boolean networks. All the main functions are described in a handy [vignette](https://cran.r-project.org/web/packages/BoolNet/vignettes/BoolNet_package_vignette.pdf).
  
  - `r pkg("egor")` allows to create ego-centric networ starting on exports from [_EgoNet_](https://github.com/egonet/egonet), [_EgoWeb 2.0_](https://www.qualintitative.com/egoweb/) and [_openeddi_](https://github.com/jfaganUK/openeddi). It includes a Shiny app and procedures for creating and visualising clustered graphs.
  
  - `r pkg("ionet")` creates network starting bt turning input-output tables into weighted adjacency matrices.
 
----

Note: While `igraph` does not have a specific structure for dynamic networks, `statnet` can manage them through `r pkg("networkDynamic")` and analyse them with `r pkg("tsna")`.

----

## Network Manipulation

Both main packages for network analysis provide similar network-manipulation capabilities, but other packages also offer a more limited set of options.

- `r pkg("tidygraph")` is designed for handling and manipulating graph data within the [_tidyverse_](https://www.tidyverse.org/) framework. It provides a tidy approach to working with relational data, allowing users to apply familiar data manipulation techniques from the tidyverse to graphs. It does not make it into the 'core' packages because it lacks a comprehensive set of tools for network analysis. Users can easily perform tasks such as filtering, summarizing, and joining graph data using familiar tidyverse syntax. Given that both `r pkg ("igraph")` and `r pkg ("statnet")`/`r pkg ("network")` provide piped functions for most operations, ``r pkg ("tidygraph")`'s added value lies mainly in the possibility of accessing directly either the node data, the edge data or the graph itself while computing inside verbs.

## Network Analysis

Both `r pkg ("igraph")` and `r pkg ("statnet")` offer functions for a similar set of network-analytic operations, whereas `r pkg ("tidygraph")` is much more limited. Amongst them, it may be worth mentioning some algorithms that differ at least slightly in the implementation and/or there are noteworthy specialised packages.

### Centrality

Both main packages can compute betweenness, eigenvalue, power, and closeness centrality, but `r pkg ("igraph")` offers more options than `r pkg ("sna")` and `r pkg ("tidygraph")` overall. In addition:

- `r pkg("centiserve")` adds dozen of centrality measures for `r pkg ("igraph")` objects such as bottleneck, decay, and entropy centrality.

- `r pkg("birankr")` provides optimised functions for estimating various centrality measures in bipartite/two-mode networks.It can also estiamte efficiently page-rank in one-mode networks, project two-mode networks to one-mode ones, and convert edge lists and matrices to the `sparseMatrix` format offered in the package `Matrix`. It supports edge lists (in the `data.frame`, `data.table::data.table`, or `tidydata::tbl_df` class) and adjacency matrices (either in the built-in `matrix` class or in `Matrix`'s `dgCMatrix` class).

# Network Modeling & Simulation

This section does not include Bayesian networks and Markov Random-Field models as they merely represent relations between variables and are listed in the CRAN TaskView on [Graphical Models](https://cran.r-project.org/web/views/GraphicalModels.html) 

- `r pkg("ergm")` provides function to fit, simulate and analyse exponential-family random graph models (ERGM). Depending on specific needs, several specialised extentions are available

|Use case|Package|
|--------|-------|
|Count weights|`r pkg("ergm.count")`|
|Egocentrically sampled networks|`r pkg("ergm.ego")`|
|Multilayer networks and samples of networks|`r pkg("ergm.multi")`|
|Rank-order networks|`r pkg("ergm.rank")`|
|Modeling ERGM-generating processes|`r pkg("ergmgp")`|
|Fit ERGM to small networks|`r pkg("ergmgp")`|
|Small hierarchical ERGMs|`r pkg("lightergm")`|
|Large hierarchical ERGMs|`r pkg("biergm")`|

- `r pkg("amen")` offer additive and multiplicative effect (AME) models with regression terms, covariance structure of the social relations model (Warner, Kenny and Stoto ([1979](https://doi.org/10.1037/0022-3514.37.10.1742)), and multiplicative factor models (Hoff [2009](https://doi.org/10.1007/s10588-008-9040-4)). It supports  binary networks as well as valued ones (assuming a Gaussian, zero-inflated/tobit, ordinal, or fixed-rank nomination model)

- `r pkg("bootnet")` implements bootstrap procedures to assess accuracy and stability of estimated network structures and centrality indices. It works on undirected network only.
  - For an alternative see `r pkg("localboot")`.

- `r pkg("dyads")` offers functions for the MCMC simulation of dyadic network models j2, p2 (also multilevel) and b2 model.

- `r pkg("fastnet")` allows to simulate large-scale social networks and retrieve their most relevant metrics following the approach proposed by  Dong, Castro, and Shaikh ([2020](https://doi.org/10.18637/jss.v096.i07)).

- `r pkg("multinets")` is an `igraph` extension to analyse multilevel networks as described in  Lazega and Snijders's book ([2016](https://doi.org/10.1007/978-3-319-24520-1)).

- `r pkg("nda")` gathers non-parametric dimensionality-reduction functions  with/out (automated) feature selection and limited plotting capabilities.

- `r pkg("lolog")` implements Latent Order Logistic (LOLOG) models, a network formation process in which edges are added one at a time drawn from a distribution conditional on edges already added, with order unknown.

## Dynamic Networks

The following packages focus on modeling and simulation of networks that evolve over time and network processes that occur over time.

### Relational Events

Relational event data contains information about exact times during which the nodes interact. This is commonly observed for e-mail, radio, and other communications.

- `r pkg("rem")` and `r pkg("relevent")` both contain functions to fit and simulate dyad-oriented relational event models. `r pkg("relevent")` can also estimate event sequence data without time stamps.

- `r pkg("goldfish")` offers functions to fit and simulate actor-oriented dynamic network actor models and dyad-oriented relational event models.

### Discrete Observations

The following packages are focused on modeling series of networks, also known as panel data.

- `r pkg("tergm")` a set of extensions for `r pkg("ergm")` for fitting and simulating discrete-time models for series of networks (or a long-term equilibrium of a discrete-time network process) where each time step is modeled as a draw from an ERGM conditional on the prior time steps.

- `r pkg("dnr")` estimation of discrete-time models for series of networks where each time-step is modeled as a draw from an ERGM conditional on prior time steps, subject to the constraint that within each time step, edge variables are independent. Varying node sets are also supported.

- `r pkg("btergm")` bootstrap inference for discrete-time models for series of networks where each time step is modeled as a draw from an ERGM conditional on the prior time steps.

- `r pkg("RSiena")` estimation of continuous-time Stochastic Actor-Oriented Models (SAOMs) for panel network data.


# Ad-hoc Packages

Being a flexible method, network analysis is used in a number of fields with specific needs addressed by ad-hoc packages.

## Ecological Networks

- `r pkg("econetwork")` is a collection of advanced functions to analyse and models of ecological networks (mainly food webs and host-parasite relations, but also plant-pollinator and other mutualistic ones) statically and dynamically (based on Ohlmann et al [2023]( https://doi.org/10.1016/j.ecolmodel.2023.110424)). 

- `r pkg("AnimalHabitatNetwork")` provides functions for generating and visualising networks representing the physical configurations of animal habitats. It implements an original  network-generating algorithm based on pair-wise Euclidean and can output undirected network either weighted or binary, fully connected or sparse). The package is associated to a PDF on modelling the physical configurations of animal habitats using networks.

- `r pkg("aniSNA")` allows to obtain network structures from animal GPS telemetry observations and statistically analyse them to assess their adequacy for social network analysis. Methods include pre-network data permutations, bootstrapping techniques to obtain confidence intervals for global and node-level network metrics, and correlation and regression analysis of the local network metrics.
  
- `r pkg("asnipe")` implements several tools that are used in animal social network analysis to cluster, and generate networks, perform permutation tests, calculate association rates, and performe multiple regression analysis.
  
- `r pkg("ATNr")` estimates _allometric trophic models_ (ATN) for the species biomasses in dynamic food-webs and allows to generate synthetic networks. It also provides access to the ODE solver deSolve.
  
- `r pkg("BIEN")` allows to access the _Botanical Information and Ecology Network Database_ in R
  
- `r pkg("bipartite")` offers functions to visualise food webs and calculate some ecological indices on them.
  
- `r pkg("cassandRa")` deals with under-sampling in ecological networks by fitting a variety of statistical models and sample coverage estimators to correct for (likely) missing ties. It works only on bipartite networks.  

- `pkg("EcoNetGen")`	to simulate and sample from ecological networks,

- `pkg("econullnetr")` to carry out  null-model analysis for ecological networks 

## Bibliometric Networks

  - `r pkg("bibliometrix")` includes functions to import bibliographic data from the main publication databases online ('SCOPUS', 'Clarivate Analytics Web of Science', 'Digital Science Dimensions', 'Cochrane Library', 'Lens', and 'PubMed'). It can also build networks (`bibliometrix::biblioNetwork`) for co-citation, coupling, scientific collaboration and co-word analysis including their dynamic versions (`bibliometrix::histNetwork`). It allows to plot the data using `VOSviewer.jar`.
  
  - `r pkg("bibliometrixData")` contains example datasets for testing `bibliometrix`.
  
  - `r pkg("biblionetwork")`	proposes functions to identify and weight the edges in a bibliometric network. All functions are optimised for large dataset. It implements different methods for different types of relations (based on Perianes-Rodriguez, Waltman, and Van Eck [2016](https://doi.org/10.1016/j.joi.2016.10.006); Leydesdorff and Park [2017](https://doi.org/10.1016/j.joi.2016.11.007)):
      - co-authorship supports: simple counting, (refined) fractional weight with or with cosine normalisation;
     - bibliographic coupling supports: coupling strength and angle;
     - co-citation supports the cosine normalisation of count weights.   

- `r pkg("Diderot")` is geared towards the analysis of citation networks using  modularity and heterocitation metrics based on Scopus data.
    
## Biology and (Bio)-Chemistry Networks

  - `r pkg("WGCNA")` focuses on the analysis of weighted correlation networks. It has functions for network construction, modularity computation, gene selection, topological analysis, generating data, plotting, and exports to third-party software. Notably, the underlying data mining approach has been used beyond biochemistry. There are several packages on Bioconductor that reverse-depend/extend these functionalities.

  - `r pkg("c3net")` allows to infer gene-regulation networks with direct physical interactions using `C3NET` (Altay and Emmert-Streib [2010](https://doi.org/10.1186/1752-0509-4-132)). Other packages implement improvements/variants of this algorithm based on the literature, such as:
  
    - `r pkg("Ac3net")` Infers directional conservative causal core in gene network based on the algorithm for directional network proposed by Altay ([2018](https://doi.org/10.1101/271031)).
    
    - `r pkg("bc3net")` implements the BC3NET algorithm for inference on gene-regulation networks  (Simoes and Emmert-Streib [2012](https://doi.org/10.1371/journal.pone.0033624)). In essence it offers a Bayesian approach with noninformative prior to the C3NET algorithm.

  - `r pkg("BioNAR")` implements a detailed topologically-based network analysis with functions that create networks based on laboratory-produced meta-data. It includes functions for vertex centrality measure and modularity computation. Additionally, it provides a robust synaptic proteome network for data validation.
  
  - `r pkg("BASiNET")`	and `r pkg("BASiNETEntropy")` provide functions for classifying RNA sequences using network algorithms and notions from information theory.
  
  - `r pkg("bionetdata")` is a collection of relation datasets of biological and chemical nature.
  
  - `r pkg("Cascade")` includes functions for gene selection, reverse engineering, and prediction in cascade networks.

## Neurosciences & Psychology

- `r pkg("NetworkToolbox")` implements network analysis and graph theory measures used in neuroscience, cognitive science, and psychology. Methods include various filtering methods and approaches such as threshold, dependency. It can also execute some basic operations such as computing centrality of nodes and community or the network's clustering coefficient.

- `r pkg("qgraph")` provides tools for visualising and analysing weighted networks and a  Gaussian graphical model for plotting. It is compatible with `r pkg ("igraph")` through the `qgraph::as.igraph.qgraph` function. It is mostly used in psycology and neurosciences.

- `r pkg("HospitalNetwork")` provides functions to construct a one-mode network of hospitals based on the linked two-mode networks of hospitalised patients' transfers.

  
## Spatial networks

- `r pkg("geonetwork")` handles networks or graphs whose nodes are locations. The functions includes the creation of objects of class `geonetwork` as a graph with node coordinates, the computation of network measures, the support of spatial operations (projection to different Coordinate Reference Systems, handling of bounding boxes, etc.) and the plotting of the `geonetwork` object combined with supplementary cartography for spatial representation. It is compatible with ``r pkg ("igraph")`.

- `r pkg("chessboard")` provides functions to work with un/directed undirected spatial networks. It allow to create connectivity matrices (`chessboard::connectivity_matrix`) and exports result to several formats: node list, neighbor list, edge list, connectivity matrix, Eigenvector maps. It also implements connectivity for chess pieces via specific functions: `chessboard::bishop`,  `chessboard::knight`, `chessboard::pawn`, `chessboard::queen`, `chessboard::rook`, besides introducing two sets of movement rules `chessboard::fool` and `chessboard::wizard`.

- `r pkg("epanet2toolkit")` interfaces R with  the [EPANET](https://github.com/OpenWaterAnalytics/EPANET/releases/tag/v2.2) programmer's toolkit to carry out basic (`epanet2toolkit::ENepanet`) or customised (`epanet2toolkit::ENopen`) simulations.

- `r pkg("intensitynet")` includes functions to analyse point patterns in space occurring over planar network structures derived from graph-related intensity measures for un/directed and mixed networks

## Public Health Networks

  - `r pkg("epinet")` simulates contact networks to predict the transmission of contagious diseases through Bayesian inference.
  
  - `r pkg("hybridModels")` offers a meta-population model that assign nodes to sub-populations to better model disease spreading through cluster contagion using stochastic simulation algorithm and an individual-based approach.
  
  - `r pkg("netdiffuseR")` provides function for calculating network effects such as transmission rate, hazard rates, exposure models, network threshold levels, infectiousness (contagion), and susceptibility. 
  
  - `r pkg ("EpiModel")` builds on Statnet's for epidemic modelling. But more on this field of application can be found in the [CTV: Epidemiology](https://cran.r-project.org/view=Epidemiology).

## Social and Economic networks

- `r pkg ("sna")` implements many operations commonly carried out on networks in the social and econonomic sciences with the ability of regress a network variable on others using ordinary least square, linear network autocorrelation models or a logistic regression.^[More on this type of applications can be found in the CRAN TaskView on [Graphical Models](https://cran.r-project.org/web/views/GraphicalModels.html)]
 
- `r pkg("FinNet")` provides classes, methods, and functions to deal with financial networks involving both physical and legal persons. The package assists in creating various types of financial networks: ownership, board interlocks, etc.. It support differnt tie-weighting procedures (valued or binary), and renders them in the most common formats (adjacency matrix, incidence matrix, edge list, `r pkg ("igraph")`, `r pkg ("statnet")`).

- `r pkg("ITNr")` gathers functions to clean and process international trade data into an adjacency matrix. It can also extract the network's backbone, compute centrality, run blockmodels and other clustering procedures, or highlight regional trade patterns.

- `r pkg("modnets")` models moderator variables in cross-sectional, temporal, and multi-level networks.

- `r pkg("multinet")` provides functions for the creation/generation and analysis of multi-layer social networks


# Visualisation

- `r pkg("visNetwork")` focuses on interactive network visualisation using the `vis.js` library. The package  allows users to create visually appealing and interactive network visualizations with features such as zooming, panning, and node highlighting. The package offers a user-friendly interface for creating interactive network visualisations, making it suitable for un-experienced users.

- `r pkg("networkD3")` provides functions that turns edge lists into a D3 JavaScript network, tree, dendrogram, or Sankey graphs.

  - `r pkg("bipartiteD3")` uses the `D3` and `viz-js` libraries for plotting networks produced with the `r pkg("bipartite")` package.
  
- `r pkg("diagram")` was born as a companion to the book _A practical guide to ecological modelling_ by K. Soetaert and P.M.J. Herman. But it can visualise any network given in the form of a transition matrix as a flow diagram, a web or grid. 

- `r pkg("ndtv")` renders network objects from the package `networkDynamic` as videos or interactive animations.

- `r pkg("neatmaps")` tries to simplify the exploratory step of data analysis by providing function to easily produce hierarchical clusterings (`neatmaps::hierarchy`), consensus clusterings (`neatmaps::consClustResTable`) and heatmaps of multiple networks (`neatmaps::neatmap`).

Extensions for `ggplot2`:

  - `r pkg("ggnetwork")` offers geometries to plot `network` objects.
  - `r pkg("ggraph")` allows to plot `igraph` objects by building up plots layer by layer.
  - `r pkg("ggsom")` offers functions to plot self-organizing maps (SOMs). 

- `r pkg("graphlayouts")` adds several layout algorithms to `r pkg("igraph")` based on the concept of stress majorisation

# Clustering

## Community detection

- `r pkg("igraph")` is the package of choice for the implementation of most modularity-based community-detection algorithms. Available approaches include betweenes, greedy algorithm, infomap, label propagation Leiden, Generalised Louvain, and walktrap amongst others.

- `r pkg("cencrne")` proposes a regularised network-embedding model to simultaneously estimate the community structure and the number of communities in an asymptotically consistent way. Them method is mainly used in biosciences, but is applicable across the board.

- `r pkg("linkcomm")` provides functions for generating, visualising, and analysing overlapping communities in networks of arbitrary size and type. Unlike `igraph` and `network`, it can compute relatedness `linkcomm::getClusterRelatedness` and `linkcomm::getCommunityConnectedness` as well as generate a mesoscopic matrix (`linkcomm::getCommunityMatrix`). Moreover, it can produce membership for hierarchical communities (`linkcomm::getNestedHierarchies`).

## Blockmodeling

### Generalised blockmodeling (structural and/or regular equivalence)

- `r pkg("sna")` implements a simple version of stuctural-equivalence blockmodel (`sna::blockmodel`), can generate networks with a given blockmodel as well as print and plot the results.

- `r pkg("concoR")` implements the classical CONCOR (CONvergence of iterated CORrelation) algorithm (Breiger, Boorman, and Arabie [1975](https://doi.org/10.1016%2F0022-2496%2875%2990028-0)) for one- and multi-mode un/directed networks.

- `r pkg("blockmodeling")`: this package offers and implementation of generalised blockmodeling (`blockmodeling::optRandomParC`) as well as functions for computation of (dis)similarities in terms of structural or regular equivalence and plotting. Furthermore, it include implementations of the REGE (also implemented in Ucinet) algorithm (`blockmodeling::REGE`).
  - `r pkg("BlockmodelingGUI")` is a Shiny app providing a graphical interface for generalised blockmodeling of single-relation, one-mode networks from the package `r pkg("blockmodeling")`. It includes several ways to visualise networks and partitions.

- `r pkg("kmBlock")` implements a k-means like approach to the blockmodeling of one-mode and linked networks as presented in Žiberna ([2020](https://doi.org/10.1016/j.socnet.2019.10.006)) based on structural equivalence.

- `r pkg("dBlockmodeling")` contains functions to apply blockmodeling of signed (positive and negative weights are assigned to the links), one-mode and valued one-mode and two-mode.

- `r pkg("signnet")` offers to functions implementing the generalised blockmodeling with structural equivalence (`signnet::signed_blockmodel`) and generalised equivalence (`signnet::signed_blockmodel_general`) of signed networks based on `graph` objects from the R package `r pkg("igraph")` 

### Stochastic blockmodeling (SBM)

- `igraph` cannot run SBMs, but it can generates a random graph according to a specified SBM (`igraph::sample_sbm`) or an arbitrary hierarhical SBM (`igraph::sample_hierarchical_sbm`)

- `r pkg("blockmodels")` allows to run the SBM or the Latent Block Model (LBM) of static networks using  a Variational Expectation Maximisation algorithm. Various `S4` functions implement three probability distributions: `BM_bernoulli` for binary data, `BM_poisson` for discrete/count weights, `BM_gaussian` for continuous weights. It allows for SBMs and LBM with or without node covariates and supports multiplex binary networks via `BM_bernoulli_multiplex`.

- `r pkg("sbm")` is an extension of `blockmodels` bi- and multi-partite as well as multiplex networks as proposed by Barbillon et al ([2017](https://www.doi.org/10.1111/rssa.12193)) through dedicated `R6` clasess. It includes functions to plot the resulting partition.

- `r pkg ("greed")` leverages a combination of greedy local search and a genetic algorithm to execute (degree-corrected) SBM and Latent Blockmodeling (LBM). 

- `r pkg("dynsbm")` implements the model for temporal networks presented in Matias and Miele ([2020](https://doi.org/10.1111/rssb.12200)) which combines a static SBM with independent Markov chains for the dynamic part. It supports binary and weighted networks with both discrete or continuous edges. Includes also functions for plotting (`adjacency.plot`, `alluvial.plot`, `connectivity.plot`) the partition and automatically constructs matrices as an array of the right format.

- `r pkg("MLVSBM")` Implements the SBM of multilevel networks where the different matrices each represent an interaction layer either weighter or binary. It generalises the approach proposed by Chabert-Liddell et al. ([2021](https://doi.org/10.1016/j.csda.2021.107179)) to more than two layers.

- `r pkg("StochBlock")` implements the stochastic blockmodeling of one-mode and linked networks as implemented in Škulj and Žiberna ([2022](https://doi.org/10.1016/j.socnet.2022.12.003)). It include utilities to plot the results, but cannot choose automatically the 'right' number of clusters and tends to be very slow according to subsequent reviews (see Cugmas and Žiberna [2023](https://doi.org/10.1016/j.socnet.2022.12.003));

-  `r pkg("GREMLINS")` implements the SBM of generalised multipartite networks where the different matrices each involve nodes that can be partitioned into  a-priori defined _functional groups_ as proposed by Bar-Hen, Barbillon, and  Donnet ([2018](https://doi.org/10.1177/1471082X20963254)).

## Others

- `r pkg("clustNet")` allows to cluster units in a network using a Bayesian mixture model that can account for node and edge covariates.

- `r pkg("collpcm")` provides MCMM inference for collapsed latent space models that allow to search over the model space, including deciding on the number of clusters.

- `r pkg("graphclust")` implements an agglomerative algorithm to maximize the integrated classification likelihood criterion and a mixture of stochastic block models based on `igraph` objects.

- `r pkg("idopNetwork")` implments the model proposed by Cao et al ([2022](https://doi.org/10.1080/19490976.2022.2106103)) to convert static data into their 'dynamic' form contextually inferring informative, dynamic, multi-directional networks with clusterable structures.

- `r pkg("latentnet")` provides functions to fit and simulate latent position and cluster model using `network` objects and compatibly with `ergm` approaches.

- `r pkg("latenetwork")` TODO

- `r pkg("netClust")` provides a function to cluster unilayer (`netClust::netEM_unilayer`) and multilayer (`netClust::netEM_multilayer`) networks by means of finite mixtures and expectation-maximisation.

# Links

* Altay, Gokmen. ‘Directed Conservative Causal Core Gene Networks’. bioRxiv, 2 March 2018. https://doi.org/10.1101/271031.

* Altay, Gökmen, and Frank Emmert-Streib. ‘Inferring the Conservative Causal Core of Gene Regulatory Networks’. BMC Systems Biology 4, no. 1 (28 September 2010): 132. https://doi.org/10.1186/1752-0509-4-132.

* Barbillon, Pierre, Sophie Donnet, Emmanuel Lazega, and Avner Bar-Hen. 2017. ‘Stochastic Block Models for Multiplex Networks: An Application to a Multilevel Network of Researchers’. _Journal of the Royal Statistical Society Series A: Statistics in Society _ 180 (1): 295–314. https://doi.org/10.1111/rssa.12193.

* Bar-Hen, Avner, Pierre Barbillon, and Sophie Donnet. 2022. ‘Block Models for Generalized Multipartite Networks: Applications in Ecology and Ethnobiology’. _Statistical Modelling_ 22 (4): 273–96. https://doi.org/10.1177/1471082X20963254.

* Batagelj, Vladimir, and Matjaž Zaveršnik. ‘Fast Algorithms for Determining (Generalized) Core Groups in Social Networks’. _Advances in Data Analysis and Classification_ 5, no. 2 (1 July 2011): 129–45. https://doi.org/10.1007/s11634-010-0079-y.

* Breiger, Ronald L, Scott A Boorman, and Phipps Arabie. 1975. ‘An Algorithm for Clustering Relational Data with Applications to Social Network Analysis and Comparison with Multidimensional Scaling’. _Journal of Mathematical Psychology_ 12 (3): 328–83. https://doi.org/10.1016/0022-2496(75)90028-0.

* Cao, Xiaocang, Ang Dong, Guangbo Kang, Xiaoli Wang, Liyun Duan, Huixing Hou, Tianming Zhao, et al. ‘Modeling Spatial Interaction Networks of the Gut Microbiota’. Gut Microbes 14, no. 1 (31 December 2022): 2106103. https://doi.org/10.1080/19490976.2022.2106103.

* Chabert-Liddell, Saint-Clair, Pierre Barbillon, Sophie Donnet, and Emmanuel Lazega. 2021. ‘A Stochastic Block Model Approach for the Analysis of Multilevel Networks: An Application to the Sociology of Organizations’. _Computational Statistics & Data Analysis_ 158 (June): 107179. https://doi.org/10.1016/j.csda.2021.107179.

* Cugmas, Marjan, and Aleš Žiberna. 2023. ‘Approaches to Blockmodeling Dynamic Networks: A Monte Carlo Simulation Study’. _Social Networks_ 73 (May): 7–19. https://doi.org/10.1016/j.socnet.2022.12.003.

* Dong, Xu, Luis Castro, and Nazrul Shaikh. ‘Fastnet: An R Package for Fast Simulation and Analysis of Large-Scale Social Networks’. Journal of Statistical Software 96 (5 December 2020): 1–23. https://doi.org/10.18637/jss.v096.i07.

* Hoff, Peter D. ‘Multiplicative Latent Factor Models for Description and Prediction of Social Networks’. Computational and Mathematical Organization Theory 15, no. 4 (December 2009): 261–72. https://doi.org/10.1007/s10588-008-9040-4.

* Lazega, Emmanuel, and Tom A.B. Snijders, eds. Multilevel Network Analysis for the Social Sciences. Cham: Springer International Publishing, 2016. https://doi.org/10.1007/978-3-319-24520-1.

* Leydesdorff, Loet, and Han Woo Park. ‘Full and Fractional Counting in Bibliometric Networks’. Journal of Informetrics 11, no. 1 (February 2017): 117–20. https://doi.org/10.1016/j.joi.2016.11.007.

* Martin, Evan A., and A. Fu. ‘Approximate Bayesian Inference of Directed Acyclic Graphs in Biology with Flexible Priors on Edge States’, 2019. https://arxiv.org/abs/1909.10678.

* Matias, Catherine, and Vincent Miele. 2017. ‘Statistical Clustering of Temporal Networks through a Dynamic Stochastic Block Model’. _Journal of the Royal Statistical Society. Series B (Statistical Methodology)_ 79 (4): 1119–41. https://www.jstor.org/stable/26773154.

* Ohlmann, Marc, Catherine Matias, Giovanni Poggiato, Stéphane Dray, Wilfried Thuiller, and Vincent Miele. ‘Quantifying the Overall Effect of Biotic Interactions on Species Distributions along Environmental Gradients’. Ecological Modelling 483 (1 September 2023): 110424. https://doi.org/10.1016/j.ecolmodel.2023.110424.

* Perianes-Rodriguez, Antonio, Ludo Waltman, and Nees Jan Van Eck. ‘Constructing Bibliometric Networks: A Comparison between Full and Fractional Counting’. Journal of Informetrics 10, no. 4 (November 2016): 1178–95. https://doi.org/10.1016/j.joi.2016.10.006.

* Simoes, Ricardo de Matos, and Frank Emmert-Streib. ‘Bagging Statistical Network Inference from Large-Scale Gene Expression Data’. PLOS ONE 7, no. 3 (30 March 2012): e33624. https://doi.org/10.1371/journal.pone.0033624.

* Warner, Rebecca M., David A. Kenny, and Michael Stoto. ‘A New Round Robin Analysis of Variance for Social Interaction Data.’ Journal of Personality and Social Psychology 37, no. 10 (October 1979): 1742–57. https://doi.org/10.1037/0022-3514.37.10.1742.

* Škulj, Damjan, and Aleš Žiberna. 2022. ‘Stochastic Blockmodeling of Linked Networks’. _Social Networks_ 70 (July): 240–52. https://doi.org/10.1016/j.socnet.2022.02.001.

* Žiberna, Aleš. 2020. ‘K-Means-Based Algorithm for Blockmodeling Linked Networks’. _Social Networks_ 61 (May): 153–69. https://doi.org/10.1016/j.socnet.2019.10.006.
