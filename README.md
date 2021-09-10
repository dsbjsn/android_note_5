# 调用系统分享

## 分享文本
```
 public static void shareApp(Context pContext,Stirng text) {
        Intent textIntent = new Intent(Intent.ACTION_SEND);
        textIntent.setType("text/plain");
        textIntent.putExtra(Intent.EXTRA_TEXT, text);
        pContext.startActivity(Intent.createChooser(textIntent, getAppName(pContext)));
    }
```
## 分享图片
```
  public static void shareApp(Context pContext, String filePath) {
        File lFile = new File(filePath);
        if (lFile.exists()) {
            Intent lIntent = new Intent(Intent.ACTION_SEND);
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N) {
                Uri contentUri = FileProvider.getUriForFile(pContext, pContext.getPackageName() + ".fileprovider", lFile);
                lIntent.putExtra(Intent.EXTRA_STREAM, contentUri);
            } else {
                lIntent.putExtra(Intent.EXTRA_STREAM, Uri.fromFile(lFile));
            }

            lIntent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION);
            lIntent.setType("image/*");
            pContext.startActivity(Intent.createChooser(lIntent, getAppName(pContext)));
        } else {
            Log.i("分享图片失败", "未找到图片");
        }
    }
```
