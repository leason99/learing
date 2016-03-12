url = new URL("https://chart.googleapis.com/chart?chl=123&cht=qr&chs=500x500");

conn = (HttpURLConnection) url.openConnection();

conn.setRequestMethod("GET");

conn.connect();

if (conn.getResponseCode() == HttpURLConnection.HTTP_OK) {

   InputStream inputStream = conn.getInputStream();

   Bitmap bitmap = BitmapFactory.decodeStream(inputStream);

   inputStream.close();

   pic.setImageBitmap(bitmap);
   }
