# RSNA Brain tumor classification

### **`Data Sources`** : 
   - [Original dataset](https://www.kaggle.com/c/rsna-miccai-brain-tumor-radiogenomic-classification/data)
   - [Preprocessed dataset](www.kaggle.com/dataset/d3537f815a48ddaef3fc70098ec98dbaa86e0d7d8eb26d331841a82c2637fc07)

`Problem Statement` : The task is to predict the genetic subtype of glioblastoma using MRI (magnetic resonance imaging) scans to train and test the model to detect  the presence of MGMT promoter methylation.

`Description` :  
 - A malignant tumor in the brain is a life-threatening condition. Known as glioblastoma, it's both the most common form of brain cancer in adults and the one with the worst prognosis, with median survival being less than a year. The presence of a specific genetic sequence in the tumor known as MGMT promoter methylation has been shown to be a favorable prognostic factor and a strong predictor of responsiveness to chemotherapy.

- Currently, genetic analysis of cancer requires surgery to extract a tissue sample. Then it can take several weeks to determine the genetic characterization of the tumor. Depending upon the results and type of initial therapy chosen, a subsequent surgery may be necessary. If an accurate method to predict the genetics of the cancer through imaging (i.e., radiogenomics) alone could be developed, this would potentially minimize the number of surgeries and refine the type of therapy required.

`Solution details` :
  - **Pre-processing** : 
    - Used library : ***TorchIO*** (Python library for efficient loading, preprocessing, augmentation and patch-based sampling of 3D medical images in deep learning, following the design of PyTorch.)
    - TorchIO helped in converting all the MRI scans to same orientation.
    - resized all images to (256 x 256)

  - **Modelling** : 
    - Densenet121 - 3D model([Monai](https://docs.monai.io/en/latest/networks.html#densenet))
    - Optimizer : Adam
    - criterion : binary_cross_entropy_with_logits
    - Trained on GPU for 15 epochs each for different MRI scans(FLAIR, T1w, T1wce, T2w).
    - Model files : [Source](https://www.kaggle.com/tharun2001/2-monoi-models-random-seeds)

  - **Post-processing** :
    - simple average ensemble of all the 4 models built with four different MRI scans.  
