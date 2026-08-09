# Railway deployment

This repository is configured to deploy the FastAPI service from the `backend/` directory through the root `Dockerfile`.

## Deploy

1. Create a new Railway project and deploy this GitHub repository.
2. Railway will detect `railway.toml` and build the root `Dockerfile`.
3. Set `CORS_ORIGINS` to the frontend origin(s), separated by commas. Example:

   `https://your-frontend.up.railway.app`

4. Deploy and verify:

   `https://your-service.up.railway.app/api/health`

Railway provides `PORT` automatically. The container binds to `0.0.0.0` and uses that value.

## Storage

Railway container storage is ephemeral. Uploaded and processed images in `uploads/` and `saved_images/` will be lost when the service is redeployed or restarted. Attach a Railway Volume and mount it at `/app/saved_images` if those files must persist, or replace local storage with an object-storage service for production use.

The TensorFlow model is packaged into the image from `backend/model/`, so no model download step is required at deploy time.
