# Music-Note-Predection

## Introduction

In this project we find the optimal machine learning model for generating potentially novel classical music in the style of a given renowned music composer.
The significance of this project is evident in its demonstration of computational and mathematical creativity, which can be leveraged to perform tasks that
have traditionally been performed by humans.

## Dataset Attributes

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


