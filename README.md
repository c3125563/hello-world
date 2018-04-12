\typeout{Annual Conference of the Prognostics and Health Management Society Style}
\typeout{Template version updated November 25, 2013}

% Please send questions regarding the Latex templates to Indranil Roychoudhury (indranil.roychoudhury@nasa.gov), Matthew Daigle (matthew.j.daigle@nasa.gov), or Anibal Bregon (anibal@infor.uva.es).



\documentclass[PHME, 2018]{PHMSociety}
% NOTE: replace '2014' above with the year of the conference you are submitting this publication to.

% Declare packages
\usepackage{graphicx}
\usepackage{amsmath}
\usepackage[numbers]{natbib}

\begin{document}
	
	% Paper Title
	\title{An auto-associative approach to identify and restore corrupted input using correlated trends}
	
	% Authors List
	\author{%			
		Peter Goldthorpe\authorNumber{1}, and Antoine Desmet\authorNumber{2}
	}
	
	% Author Affiliations
	\address{% This is a tabular environment so each affiliation needs to be separated by "\\" or "\tabularnewline"
		\affiliation{1}{University of Newcastle, Newcastle, NSW, 2308, Australia}{ %add emails
			{\email{Peter.Goldthorpe@newcastle.edu.au}}
		} % emails input
		\tabularnewline % skip one row for next affiliation	
		\affiliation{2}{Komatsu Mining Corporation, Rutherford, NSW, 2320, Australia}{ % add emails
			{\email{Antoine.Desmet@mining.komatsu}}
		} % emails input
	}
	
	
	% Create the title
	\maketitle
	\pagestyle{fancy}
	\thispagestyle{plain}
	
	
	% PHM Society Distribution License Information, provide first author's name "FirstName LastName"
	% NOTE: Do not forget to add this. The paper will not be accepted without this open access license footnote.
	\phmLicenseFootnote{Peter Goldthorpe}
	
	%===================================================================%
	%																	%
	%					 			Abstract							%
	%																	%
	%===================================================================%
	
	% Abstract
	\begin{abstract}%   %NOTE: Deleting the percentage after "{abstract}" may be lead to an extra leading space in the first line of the abstract, and this should be prevented.
		Lorem ipsum dolor sit amet, consectetur adipiscing elit. In finibus finibus enim eget ullamcorper. Nulla convallis luctus est, tincidunt semper nibh vestibulum a. Curabitur hendrerit finibus faucibus. Ut vel urna pharetra, tempor lacus bibendum, posuere ante. In porta at neque ac rutrum. Phasellus dictum orci at lorem bibendum pretium. Mauris ut dui nibh.
		
		Cras scelerisque sollicitudin lacus, et varius nunc aliquet quis. Pellentesque porttitor augue nec facilisis dignissim. Suspendisse semper sollicitudin sollicitudin. Nunc egestas vitae metus ac vulputate. Cras rutrum fringilla metus eget fermentum. Phasellus finibus tortor congue lacus suscipit blandit. Duis porttitor dolor at varius cursus. Curabitur quis velit sed ante auctor varius tincidunt fringilla urna. Vestibulum condimentum in ligula eget posuere. Donec in gravida nibh. Nunc eget risus lacus. In sollicitudin nec ante ac suscipit. Ut fermentum vitae diam ut auctor.
		
		Aenean tempus, erat id rhoncus molestie, justo mauris tristique massa, nec commodo neque dolor in tortor. Nunc sit amet ultrices leo. Maecenas consequat augue in nisi porttitor, eget ullamcorper purus iaculis. Vestibulum ac eleifend turpis. Sed odio mauris, ullamcorper sed velit ac, condimentum tincidunt velit. Sed finibus nulla elit. Etiam mattis velit eu elit porta, in auctor libero consectetur. Suspendisse mollis, quam eget dignissim egestas, odio magna faucibus elit, non sagittis velit odio non tortor. Suspendisse a nisi ut ligula sodales eleifend sed vitae nisl. Nunc consequat rutrum augue et tincidunt. In hac habitasse platea dictumst.
		
		Curabitur accumsan sed dui ac lobortis. Aliquam sed diam feugiat, tincidunt est non, interdum enim. Suspendisse purus nulla, sodales sit amet maximus varius, congue ac turpis. Pellentesque a porta dui, ac bibendum erat.
	\end{abstract}

	%===================================================================%
	%																	%
	%					 		1. Introduction							%
	%																	%
	%===================================================================%

	\section{Introduction}
	%% Benefits of data analysis
	% Why data analysis is useful and should be investigated by businesses
	% Advantages of performing big data analyses
	More data are being recorded now than any other time in history. With the improvements in technology and the reduction in hard drive costs, computers are now able to cheaply store large amounts of data. Companies are able to utilize this large storage capacity to keep a record of products over time. In the mining industry, large machinery are equipped with hundreds of sensors that repeatedly sample phenomena from the environment and return information on its surroundings. Sensor data can be analyzed to uncover hidden trends within a machine and give a clear representation of machine health over time. The analysis of data is beneficial as it leads to data-driven business decisions that improve the quality of products and services.
	
	%% Data dependence / correlation / redundancy
	% Data sometimes model the same underlying phenomena
	Each sensor measures a unique environmental factor, but some sensors jointly collect information on the same underlying phenomena. These sensors are said to exhibit dependence. Sensors exhibit varying levels of dependence, from being entirely independent to highly correlated. Sensors that share a highly correlated dependence form groups which have an added benefit of verifying the integrity of each channel in the group. This creates a redundancy of data; channels can be represented as a lower dimension and rebuilt through known relationship to other sensors. Therefore, it is possible to infer a channel within a group given the channel’s relationship to the group. This paper will focus on highly correlated data, where groups of sensor data represent inputs with a high dependence and share the same lower dimensional basis.

	%% “Regular” data vs faulty data
	% What constitutes normal data?
	% Relationships mined during healthy data
	We determine the strength of dependence between inputs by mining large datasets for relationships. By observing a time series of healthy data, we can measure relationships within channels when machinery is working correctly. This gives us a baseline to compare against when data behaves differently to healthy data as broken group patterns may indicate a departure from normality. The cause may be due to various reasons: a faulty sensor, change in the underlying relationship, or difference in environment, representing a fault or failure.
	
	\begin{description}
		\item[Faulty sensor] Sensor data is inferred through electronics. One source of faulty data may be due to poor connectivity in a wire. If a sensor is faulty then values from the surrounding environment may be incorrectly recorded and mistaken as a fault in the environment. Expert knowledge can isolate a sensor fault. For example a reading that is impossibly low or high may indicate a fault in the electronics of a sensor instead of the environment.
		
		\item[Change in relationship] An apparent fault appears when the healthy mined relationships are no longer valid. Patterns are mined given a set of externally constant parameters. Once the parameters change the relationship may not be valid and relationships need to be mined again. This is not a fault but instead the model no longer works and needs to be reevaluated.
		
		For example a machine's health may be measured with a quantity of oil. The machine undergoes maintenance and has n oil replacement. This changes the correlation/dependence pattern and is marked as an apparent fault. While there is no error with the sensing equipment or an environmental phenomenon, the relationship that was inferred with healthy data has changed so new relationships must be mined with new set of parameters to correctly model a phenomena.
		
		\item[Environmental fault] Lastly a fault can occur when an environmental factor has changed compared to healthy data. This could occur when a component is broken, deteriorating and leading to a fault. This is the type of fault that we are most interested in predicting as it determines a change in the environment, and can be solved with an intervention, such as replacing a deteriorating or broken part.
	\end{description}

	We are interested in detecting genuine faults preemptive to a failure; when parts of a machine are faulty and need to be fixed. It is important to know the differences in faults and where they apply, to avoid wasting time and spending money attempting to fix the wrong problem.
	
	\begin{figure}
		\includegraphics[width=\linewidth]{ann.png}
		\caption{Artificial Neural Network.}
		\label{fig:ann}
	\end{figure}

	%% Current methods
	
	% Need to fix this bad paragraph.
	%======================================%
	The current modeling techniques for fault detection involves creating a model which recreates how dataset should work under healthy conditions, then comparing to the model to determine deviation from healthy data. Large deviations indicate a departure from normality. A model which recreates the inputs is called an autoassociative model. This type of model reconstructs the input when things are working normally. 

	
	When modeling highly correlated data with a corrupt channel, current models encounter a problem called spillover. Spillover is an error induced when faults in a single input propagate through a model and corrupt the group reconstruction of channels. For healthy data the error between raw data and model should be minimal or nonexistent. Spillover is a problem as it dilutes the error into other channels.
	%======================================%	
	We best demonstrate the idea of spillover with an example. Suppose we have four channels each with an arbitrary value {x}. Because the values are all highly correlated we perform a dimensionality reduction and reduce to a single value, the mean, which takes the value of {x} which we use to rebuild the four channels. Suppose one of the channels instead has an error term {a} so the channel has a corrupt value of {x+a}. The mean of these values becomes {x+a/4}. When we reconstruct the inputs, the three healthy channels have an induced error of {a/4}. The error "spills over" to the non-faulty channels.
	
	In Figure~\ref{fig:raw1} we have raw data with an error in a single channel. The purple curve shows the mean of all channels. Because of an error in the blue channel, the mean is artificially high. Subtracting the mean gives the reconstruction error in Figure~\ref{fig:recon1}.
	
	% Introduced the word "coding" without giving a definition
	%========================================================%
	Spillover is especially apparent in dimension reduction problems. Highly correlated data are susceptible to spillover as all channels contribute some part to the coding. If one channel is faulty this corrupts the coding and the error induces spills over to basis dimension that reconstructs all channels.
	%========================================================%
	
	The spillover effect is inversely proportional to the number of channels in a group. A larger number of channels is less susceptible to spillover as error in a single channel 1/n of the spillover effect to other channels. There are two ways to minimize or remove spillover. The first method is by adding a larger number of correlated channels to a model. This is done by increasing the number of sensors recording the underlying phenomena and validating the current channels. This is not practical as it is wasteful and duplicates the sensor; the current channels already have a high redundancy. Our focus is on the second method, finding a model that independently scans and validates each channel to avoids spillover.
	
	\begin{figure}
		\includegraphics[width=\linewidth]{rawval_error.png}
		\caption{Raw Data.}
		\label{fig:raw1}
		
		\includegraphics[width=\linewidth]{recon_error.png}
		\caption{Reconstruction Error.}
		\label{fig:recon1}
	\end{figure}


	%===================================================================%
	%																	%
	%					 	2. Literature Review						%
	%																	%
	%===================================================================%
	
	\section{Literature Review}
	Current methods for fault detection and isolation in highly correlated data have shown success but these models are involved or susceptible to spillover. We investigate a broad range of models and their suitability for our task as an improvement on the current models.
	
	\subsection{Expert Models}
	The most time consuming model is one manually coded by an expert. A human writes rules that describe their perception of normal operation into code and this code is run to detect anomalies. As the working environment of each machine is different, a new model may be required for each machine. This is time consuming and subject to human error and requires experience and good knowledge of the data to place in manual checks. Preferably we would search for a model that can be easily generalized and automatically trained on data from the same machine.
	
	\subsection{Clustering}
	
	% Need more familiarity on clustering techniques to provide a high level overview. Will get back to this.
	%==========================================%
	Clustering is a common anomaly detection technique. Train clusters on normal data then for every new point check to see how far from clusters of normality.\cite{desmet2017leak}
	%==========================================%

	\subsection{Artificial Neural Network}
	One of the most powerful and versatile machine learning models is an artificial neural network (ANN). Many models can be described in terms of an ANN. At a high level, an input layer is passed through a number of hidden layers before returning a desired transformed output. An artificial neural network is a flexible model where inputs are transformed to hidden layers with different levels of abstraction. \cite{lecun2015deep}
	
	\subsubsection{Univariate Autoregressive Model}
	An autoregressive model is a time series technique that uses the sum of weighted coefficients from previous time measurements to predict future values. \cite{fitzmaurice2008longitudinal} An autoregressive model is most suitable for modeling periodic trends: where an effect is most apparent from previous time measurements.	As many phenomena are dependent upon operation of the machine they appear at irregular intervals as the machine is operated. An example is starting and stoping at arbitrary times. A univariate autoregressive model is unsuitable for our application as machines are not time independent. 
	
	\subsubsection{Autoassociative Model}
	An auto associative model maps an input performs an identity mapping given some restraint. In general  dimensionality reduction where the input layer is mapped to a lower dimension manifold then rebuilt from the lower dimension layer, also known as codings. \cite{goodfellow2016deep} The information is placed into a smaller layer by an encoder and retrieved by a decoder. This nomenclature will be used later in the paper when discussing dimensionality reduction. An autoassociative model is a suitable model as we aim to rebuild an equal number of channels to those entered in the model. Another advantage of autoassociative models provides fast and flexible mappings. Once the coding level has been trained, only a simple matrix multiplication is required to transform an original dataset.There are 3 autoassociative models we will cover below.

	\paragraph{Principal Component Analysis}
	% Projection to a linear manifold in higher dimensional space. Form a lower dimensional subspace. Lose information in the remaining orthogonal directions.
	(PCA) is a form of dimensionality reduction which performs a linear mapping to a set of lower dimensional basis vectors, where axes are selected in descending order of maximized variance. The least explained dimensions are dropped, and the model is reconstructed from a lower number of dimensions. This ensures maximum information about the dataset is retained. \cite{geron2017hands} This method is useful to address the highly correlated redundancy issue as minimal information is lost when mapping N highly correlated inputs to a single thing. \cite{christopher2016pattern} PCA has limitations that it is only linear mapping. While this is useful for our task we aim to improve upon this method. 
	
	\paragraph{Autoencoder}	
	 is another auto-associative artificial neural network which is tasked with mapping inputs to the outputs given some restriction on the reconstruction. Similar to PCA, an autoencoderallows for advanced nonlinear mappings. Where PCA maps only to a linear manifold, an Autoencoder allows mapping to a curved manifold. Only the most relevant input information is kept while redundant information is dropped. A single hidden layer with linear activation and mean squared error (MSE) loss function is equivalent to PCA.
	
	% Room for improvement
	%===========================
	Among the autoencoders exists a type called a denoising autoencoder. A denoising autoencoder is trained to map inputs (to nearby manifold) This performs in a similar method to how clustering maps a nearby point to the nearest cluster. Denoising autoencoder is a more robust autoencoder less susceptible to corruption from single inputs as it attempts to map values to max likelihood within a small region.
	
	Denoising autencoders are used in MNIST dataset. Errors in the image are
	%===========================
	
	\paragraph{Hierarchical Extreme Learning Machines}
	There has been promising research into Hierarchical Extreme Learning Machines (HELMs). The HELM is for the detection and isolation of faulty channels in correlated inputs similar to an autoencoder for the dimensionality reduction \cite{michau2017deep} \cite{hope2017learning}. The hidden layer, or coding, is trained then examined separately to a level of normal data and.... Both methods are worth exploring further, but for this paper we choose to investigate a denoising autoencoder.
	
	%===================================================================%
	%																	%
	%					3. Hypothesis / Methodology						%
	%																	%
	%===================================================================%
	
	\section{Hypothesis / Methodology}
	\subsection{Hypothesis}
	The purpose of this paper is to create a denoising autoencoder to objectively scan and validate individual inputs in highly correlated data. The autoencoder will surgically remove noise from abnormal inputs to reconstruct a correctly working model. By harnessing the denoising effect to map faulty inputs to their expected value, the denoising autoencoder should avoid the spill-over effect induced in other models.
	
	\subsection{Preparing data}
	\subsubsection{Collecting data}
	Data were queried from Komatsu Mining Corp databases on four highly correlated motor temperatures for a wheel loader machine. 28 days of data were collected from the 10th November to 8th December 2017 with a sampling rate of 100ms, giving a total of 3545799 time points. Only changes in temperature of 1C or greater were recorded, leading to a large amount of missing data. Realistically the temperature changed at most once every second so most time stamps had unrecorded data where one channel updated but and other three remained unchanged.
	
	\subsubsection{Cleaning and resampling data}
	 The data were re-sampled to a rate of 30 seconds. Within each period the median of non-missing values was used as a placeholder. The median was chosen over mean to reduce the significance of outliers from faulty data. Re-sampling reduced the number of points in the 28 day period down to 56484. Missing data were filled by last observation carried forward (LOCF).
	
	November data exhibited healthy behaviour with no faults and was chosen as the training data with 40503 points (71.7\% of the dataset). In December an intermittent fault became apparent in one of the channels. The temperature was unrealistically high, increasing by over 80 degrees in seconds, and determined as a sensor error. As this was a good test for a known fault in a single channel the December data was chosen as the test data, consisting of 15982 points (28.3\% of the dataset).
	
	\begin{figure}
		\includegraphics[width=\linewidth]{nov.png}
		\caption{Loader temperature data November 2017}
		\label{fig:nov1}
		
		\includegraphics[width=\linewidth]{dec.png}
		\caption{Loader temperature data December 2017}
		\label{fig:dec1}
	\end{figure}

	\subsection{Setup and experiment}
	A denoising autoencoder was written in Python using the Google TensorFlow library. \cite{zaccone2017deep} The autoencoder was trained by individually introducing errors into four channels of healthy data and mapping to the original clean data.
	
	In each batch of the training data was separated into 5 parts. The dataset was shuffled where 20\% of the data was injected a normal distribution of error with standard deviation 50.	The dataset was shuffled again and passed into the denoising autoencoder to avoid any possiblity of learning time dependence patterns.
	
	In each batch the errors and magnitude of errors were randomised in a single random channel. The data were separated into 5 parts with a fault in the 1stThis was done so the autoencoder did not learn patterns
	
	The dataset was shuffled in two ways: first randomly selected values were injected with an error. The dataset was shuffled to avoid learning unreliable time series trends and fed through the denoising autoencoder.
	
	\subsubsection{Hyperparameters}
	Attention turned to tuning hyperparameters for the optimal denoising autoencoder model. Adjustable parameters were grouped into two categories: convergence rate and minimization. Learning rate and initialization are indicators of convergence. variables were weights and biases initialization, network architecture, activation function, loss function, number of epochs and learning rate.
	
	The autoencoder used ADAM optimizer \cite{kingma2014adam} and the loss function was the mean squared error (MSE) as recommended by sources on crafting denoising autoencoders \cite{geron2017hands} \cite{goodfellow2016deep}.
	
	The network architecture and activation function are examples of creating an overall improved performance of the model, and adjustment of these hyperparameters minimizes the MSE.
	
	\begin{description}
		\item[Network architecture] Arguable the single most important feature of model selection, the network architecture required the most fine tuning as there was a large number to choose from. It is important to ensure all architectures are tested to find the optimal network as ... This model determined how much dimension reduction. Because the channels are highly correlated and redundant, the first architecture began with a single hidden layer of one hidden node. Model increased number of nodes in the hidden layer up to 100, then 2 additional layers were added with up to 10 nodes per layer.
		
		\item[Activation function] What set the autoencoder apart from PCA was the choice of activation functions in hidden layers. Among the activation functions chosen were sigmoid, leaky rectified linear unit (leaky RELU). The leaky RELU was tested with different leaks in steps of 0.05. A leak of 0 corresponded to a linear activation function.
		
		\item[Learning rate and optimizer] 10-fold magnitude change between 1e-6 and 0.1. ADAM optimisation was recommended from other papers so was selected for this paper. Learning rate coupled with ADAM optimizer and Xavier initialization had fast convergence with a high consistency of reaching convergence thing after 5000 epochs. For this reason, 10000 epochs were set for training the model.
		
		\item[Weights and Biases] were initialized using Xavier initialization: weights were sampled from a truncated normal distribution with standard deviation of 0.1, and biases were initialized to a constant value of 0.1. \cite{glorot2010understanding}
	\end{description}
	
	Each time a set of hyperparameters was chosen, the model was run 3 times to ensure consistency in results. There were no abnormal
	
	
	%===================================================================%
	%																	%
	%					 		4. Results								%
	%																	%
	%===================================================================%
	
	
	\section{Results}
	Three main discoveries emerged from modeling highly correlated inputs using a denoising autoencoder.
	
	\subsection{Larger network topologies provided no benefit to the model}
	Though the denoising autoencoder was performed on different network architectures, advanced networks provided no improvement to the model. The performance of complex arrangements rivaled the simplest architecture, which belonged to a single hidden layer with one node. Compared to an architecture of 3 hidden layers with 5 nodes per layer (and all architectures in-between), there was no improvement to the model. Nor when the model became deeper did the any improvements take shape. This reduced the model to a single inner coding of one node.
	
	The inherent nature of the high correlation between channels This would be due to the highly correlated nature of the healthy correlated data. Because of the high correlation a healthy model is able to be represented by a single node any further nodes in the layer become redundant.
	
	\subsection{Nonlinear activation functions performed poorer than their linear counterparts}
	Nonlinear activations functions provided no benefit to the model. The model had greatest performance with a linear activation function. Models with a nonlinear activation function actually performed worse than their linear counterparts. A leaky RELU activation function with various leaks made no effect on the model. The lack of effect with leak is due to the simple linear nature of the network. The error in the model was minimised when the activation functions of the denoising autoencoder are linear.
	
	\subsection{The denoising autoencoder “blurred” instead of surgically removing the abnormal effect}
	The third discovery is a direct consequence of the first two discoveries. The minimal topology with a linear activation function performed almost equivalent to PCA. This is due to having a single node in the hidden layer. Upon reconstruction the codings received input from each of the channels. Since there was only one hidden node, if one of the input channels was corrupted this spillover to the coding, and hence induced spillover effect instead of isolating and ignoring faulty channels.
	
	Denoising autoencoder attempted to map to a highest likelihood value (like clustering).
	
	%===================================================================%
	%																	%
	%					 		5. Conclusion							%
	%																	%
	%===================================================================%
	
	\section{Conclusion}
	\subsection{Findings}
	The largest finding from this project is the denoising autoencoder did not surgically remove errors from the individual channels in highly correlated data. Instead the model continued to be affected by spillover. This was due to the larger network topology providing no benefit to the model.
	
	% Expand on this eg. Only errors in a single channel were considered
	This was unexpected behaviour. The denoising autoencoder was thought to remove target channels when the model had a larger architecture and nonlinear activation functions. Nonetheless the model made no improvement with an increasing architecture. 
	
	\subsection{Future Work}
	
	% Expand on this.
	PCA and autoencoder use the mean of all values to rebuild. Median is a possibility. Future work would look at using the median effect instead of the mean.
	
	Because the denoising autoencoder proved susceptible to spillover in highly correlated data, further attention may turn to Hierarchical Extreme Learning Machines which have shown promise in the area of fault isolation.
	
	\bibliographystyle{alpha}
	\bibliography{refs}
	
\end{document}


