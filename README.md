# EC601-MiniProject2 -- Cats VS Dogs 

Basically this project is based on transfer learning to train a simple classifier to classify images of cats&dogs. <br>
Refereral: https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/?utm_campaign=chrome_series_machinelearning_063016&utm_source=gdev&utm_medium=yt-desc#0 <br>
## 1. Set up <br>
### Clone this Repository<br>
        git clone https://github.com/qzhizhou/EC601-MiniProject2 
        cd EC601-MiniProject2 

## 2. Retrain the NetWork
### Configuration
        IMAGE_SIZE=224 
        ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}" 

### Start Tensorboard
        tensorboard --logdir tf_files/training_summaries & 

### Run the Trainging
        python -m scripts.retrain \
        --bottleneck_dir=tf_files/bottlenecks1 \
        --how_many_training_steps=500 \
        --model_dir=tf_files/models/ \
        --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
        --output_graph=tf_files/retrained_graph.pb \
        --output_labels=tf_files/retrained_labels.txt \
        --architecture="${ARCHITECTURE}" \
        --image_dir=tf_files/photos 
        
## 3. Classifying an image
        python -m scripts.label_image \
        --graph=tf_files/retrained_graph.pb  \
        --image=tf_files/photos/cats/cat.100.jpg 





