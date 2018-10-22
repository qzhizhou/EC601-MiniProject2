# EC601-MiniProject2 -- Cats VS Dogs 

Basically this project is based on transfer learning to train a simple classifier to classify images of cats&dogs. <br>
Refereral: https://codelabs.developers.google.com/codelabs/tensorflow-for-poets/?utm_campaign=chrome_series_machinelearning_063016&utm_source=gdev&utm_medium=yt-desc#0 <br>
## 1. Set up <br>
### Clone this Repository<br>
        git clone https://github.com/qzhizhou/EC601-MiniProject2 
        cd EC601-MiniProject2 

## 2. Retrain the NetWork with MobileNet model:
### Configuration
        IMAGE_SIZE=224 
        ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}" 

### Start Tensorboard
        tensorboard --logdir tf_files/training_summaries & 

### Run the Trainging
        python -m scripts.retrain \
        --bottleneck_dir=tf_files/bottlenecks \
        --how_many_training_steps=500 \
        --model_dir=tf_files/models/ \
        --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
        --output_graph=tf_files/retrained_graph.pb \
        --output_labels=tf_files/retrained_labels.txt \
        --architecture="${ARCHITECTURE}" \
        --image_dir=tf_files/photos 
        
### Classifying an image
        python -m scripts.label_image \
        --graph=tf_files/retrained_graph.pb  \
        --image=tf_files/photos/cats/cat.100.jpg 

## 3. Retrain with Inception Model :
### Run the trainging
        python3.6 -m scripts.retrain2  \
        --output_graph=tf_files/output_graph.pb \
        --output_labels=tf_files/retrained_labels2.txt \
        --image_dir=tf_files/photos/ \
        --summaries_dir=tf_files/retrain_logs \
        --bottleneck_dir=tf_files/Bottleneck2  \
        --how_many_training_steps=1000 \
        —-learning_rate=.01 \
        --training_batch_size=600\
        —-validation_batch_size=300
      
### Classifying an image
        python3.6 -m scripts.label_image2 \
        --image=tf_files/photos/cats/cat.99.jpg \
        --graph=tf_files/output_graph.pb \
        --labels=tf_files/retrained_labels2.txt \
        --input_layer=Mul \
        --output_layer=final_result




