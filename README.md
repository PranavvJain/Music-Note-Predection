# Music-Note-Prediction

## Introduction

In this project we find the optimal machine learning model for generating potentially novel classical music in the style of a given renowned music composer.
The significance of this project is evident in its demonstration of computational and mathematical creativity, which can be leveraged to perform tasks that
have traditionally been performed by humans.

## Dataset Attributes

MusicNet Dataset : https://www.kaggle.com/datasets/imsparsh/musicnet-dataset

The dataset comprises a metadata file and CSV files corresponding to individual songs. The attributes are detailed below:

### Song-Level Attributes (from CSV files)
- **start time (integer):** The precise moment in the recording when a musical note begins.  
- **end time (integer):** The precise moment when the musical note ends.  
- **instrument (integer):** The instrument that plays the note, encoded as an integer.  
- **start beat (integer):** The musical beat at which the note begins, relative to the overall tempo.  
- **end beat (integer):** The beat at which the note ends.  
- **note value (string):** The value representing the relative length of the note (in beats).  
- **note (integer):** The musical pitch being played, represented as MIDI note numbers.  
  > **Note:** This is the target attribute that the model has to predict using all the other attributes as input.

### Metadata-Level Attributes
- **Composer Name:** Name of the composer.  
- **Composition Name:** Title of the composition.  
- **Movement:** Specific section of the composition.  
- **Ensemble:** Set of instruments used to play the song.  
- **Duration:** Total length of the song in seconds.  

### Excluded Attributes
The following metadata attributes are excluded as they are not relevant to the song itself:  
- **Source of the recording**  
- **Transcriber Name**  
- **Catalog Name**

## Deep Learning Techniques with MusicNet Dataset

MusicNet is a prominent dataset in the domains of music generation and music information retrieval (MIR). It comprises 330 classical music recordings with detailed symbolic annotations, including pitch, instrument labels, and note timings. These features make it suitable for tasks such as:  
- **Multi-pitch Estimation**  
- **Instrument Recognition**  
- **Music Transcription**  

### Role of MIDI Representation  
MIDI (Musical Instrument Digital Interface) files play a vital role in music generation tasks as they provide a structured representation of music. They capture:  
- Notes  
- Timings  
- Dynamics  

MIDI files enable efficient encoding and decoding of music for machine learning models and are integral to datasets like MusicNet.

### Applications in Deep Learning  
Deep neural networks such as **Recurrent Neural Networks (RNNs)** and **Convolutional Neural Networks (CNNs)** leverage MIDI representations for:  
- Music Generation  
- Multi-pitch Detection  
- Note Sequence Prediction  

These models utilize MusicNet to learn and predict the next note in a sequence, ensuring accurate pitch and timing through structured MIDI representations.

### Challenges with MusicNet  
- **Annotation Complexity:** Manual annotations may have inaccuracies, especially in pieces with complex polyphony or fast tempos.  
- **Dataset Bias:** The dataset is heavily skewed towards classical music and piano pieces, limiting generalization to other genres.

Despite these challenges, MusicNet remains a pivotal resource for training deep learning models to understand the structure of classical music.

## Data Preprocessing

As the dataset consists of vast amounts of data, we considered limiting ourselves to songs of only one composer (i.e., Mozart) as of now for ease of implementation.

- The first step of preprocessing was to collect all the files corresponding to the selected composer and introduce a new column named `id` which identifies the song.  
- The next step was to join the metadata file and all the CSV files for the songs for the composer on the attribute `id`. This would create the final dataframe consisting of attributes from both the metadata file and CSV files for individual songs.  
- After obtaining the final dataframe, we one-hot encoded the non-numerical features, namely `composition`, `movement`, `ensemble`, and `note value`, and normalized the features using **z-score normalization**.

## Methodology and Model Details

As explained in previous sections, the attribute (label) to be predicted is the **note** to be played, given features such as timing, beat, duration of the note, and other attributes. The prediction of notes can be approached in two ways:  
1. **Regression:** Outputs a continuous value which can be rounded to the closest possible note. If the value is out of range, it is assigned the highest or lowest possible note.  
2. **Classification:** Treated as a multi-class classification problem, where each data point is classified to its respective note.  

### Approach  
- We considered a specific song (ID: `1788`) and attempted to recreate it using the predicted notes.  
- The actual notes in the song were replaced with the notes predicted by the model to analyze what the model would have played instead of the composer.  
- The final CSV file with the predicted notes was converted to a MIDI file using a custom program, enabling the generated music to be played and evaluated.

### Models Implemented  
The models tested and implemented are as follows:  
- **Linear Regression**  
- **Decision Tree Classifier**  
- **Softmax Classifier** (for multi-class classification)  
- **Random Forests**  
- **MLP Classifier**  

## Results and Performance Metrics

We used five different models to predict notes based on specific feature values: **start time, end time, instrument, start beat, end beat, and note value** from the chosen file (`1788.csv`).  
Performance metrics such as Accuracy, Precision, Recall, F1-score, and Macro F1-score were calculated to evaluate and compare the models. The following table summarizes these metrics:

| Metric        | Linear Regression | Decision Tree | Softmax Classifier | Random Forest | MLP Classifier |
|---------------|-------------------|---------------|---------------------|---------------|----------------|
| **MSE**       | 102.53            | -             | -                   | -             | -              |
| **MAE**       | 8.15              | -             | -                   | -             | -              |
| **RMSE**      | 10.13             | -             | -                   | -             | -              |
| **R Squared** | 0.0781            | -             | -                   | -             | -              |
| **Accuracy**  | 0.0340            | 0.2996        | 0.0914              | 0.4614        | 0.6492         |
| **Precision** | 0.0320            | 0.2960        | 0.0863              | 0.4597        | 0.6487         |
| **Recall**    | 0.0340            | 0.2814        | 0.0914              | 0.4638        | 0.6448         |
| **F1 Score**  | 0.0202            | 0.2888        | 0.0736              | 0.4604        | 0.6401         |
| **Macro F1**  | 0.0089            | 0.2858        | 0.0447              | 0.4689        | 0.6354         |




