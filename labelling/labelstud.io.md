# Labelstudio

Configurer une instance docker de labelstudio en mappant un repertoire local :
```bash
docker run -it -p 8080:8080 --restart always --env LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED=true --env LABEL_STUDIO_LOCAL_FILES_DOCUMENT_ROOT=/label-studio/files -v /mnt/c/BUSDATA:/label-studio/files -v /mnt/c/BUSDATA/Labelstudio/v1.4/Data:/label-studio/data --name labelstudio_1.4 heartexlabs/label-studio:latest label-studio
```
