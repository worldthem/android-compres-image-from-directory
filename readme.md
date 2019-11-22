# The example bellow will Crop and Compress image in android by path

spending a loot of time try to understand how to compress images from directory and finaly get to the working version find it bellow

use it  like
mimifyImage("imageName.jpg");



```  
public void compressImage(String finalFileName){
      //mypicture is a folder in Pictures
        String pathName =  getDirFile("mypicture").getPath()+ File.separator +"Picture_"+finalFileName+".jpg";
      
        Bitmap myBitmap =  BitmapFactory.decodeFile(pathName);
        final int maxSize = 1100;
        int outWidth;
        int outHeight;
        int inWidth = myBitmap.getWidth();
        int inHeight = myBitmap.getHeight();
        if(inWidth > inHeight){
            outWidth = maxSize;
            outHeight = (inHeight * maxSize) / inWidth;
        } else {
            outHeight = maxSize;
            outWidth = (inWidth * maxSize) / inHeight;
        }

        Bitmap resizedBitmap = Bitmap.createScaledBitmap(myBitmap, outWidth, outHeight, false);


        try {
            // File f = new File(getDirFile("CameraAPIDemo").getPath()+ File.separator +"Picture_newwwwww.jpg"  );
             //f.createNewFile();

            File f = new File(pathName);

            ByteArrayOutputStream stream = new ByteArrayOutputStream();
            resizedBitmap.compress(Bitmap.CompressFormat.JPEG, 90, stream);
            byte[] byteArray = stream.toByteArray();

            //write the bytes in file
            FileOutputStream fos = new FileOutputStream(f);
            fos.write(byteArray);
            fos.flush();
            fos.close();

        } catch (Exception error) {
            Log.d( MainActivity.DEBUG_TAG, "File not saved: " + error.getMessage());
        }

}


 public File getDirFile( String pathName) {
        File sdDir = Environment
                .getExternalStoragePublicDirectory(Environment.DIRECTORY_PICTURES);
        return new File(sdDir, pathName);

    }
    
```
