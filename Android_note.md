#### 模拟器联网

```
emulator -avd Pixel_2_API_28 -dns-server 8.8.8.8,114.114.114.114
```
Pixel_2_API_28在.android/avd中

```java
# Go to Activity
startActivity(new Intent(CrtActivity.this,DstActivity.class));
```



#### 获取位置

```java
LocationManager locationManager = (LocationManager) getSystemService(Context.LOCATION_SERVICE);
        if (ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED && ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_COARSE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
            ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.ACCESS_COARSE_LOCATION,Manifest.permission.ACCESS_FINE_LOCATION},1);
        }
        Location location = locationManager.getLastKnownLocation(LocationManager.GPS_PROVIDER);
        double lat = location.getLatitude();
        double lon = location.getLongitude();
```



#### 关于本机IP

android把127.0.0.1当作模拟器本机，而把计算机本地IP设为10.0.2.2

#### 异步请求

```java
private void getDataAsync() {
    OkHttpClient client = new OkHttpClient.Builder()
                .connectTimeout(3, TimeUnit.SECONDS)
                .build();
    FormBody.Builder formBody = new FormBody.Builder();//创建表单请求体
    formBody.add("username","zhangsan");//传递键值对参数
    Request request = new Request.Builder()
            .url("http://10.0.2.2")
            .post(formBody.build())
            .build();
    client.newCall(request).enqueue(new Callback() {
        @Override
        public void onFailure(Call call, IOException e) {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    Toast.makeText(LoginActivity.this,"请求失败了呦！",Toast.LENGTH_LONG).show();
                }
            });
        }

        @Override
        public void onResponse(Call call, Response response) throws IOException {
            if(response.isSuccessful()){//回调的方法执行在子线程。
                Log.d("kwwl","获取数据成功了");
                Log.d("kwwl","response.code()=="+response.code());
//                    Log.d("kwwl","response.body().string()=="+response.body().string());
                final String res = response.body().string();
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        Toast.makeText(LoginActivity.this,res,Toast.LENGTH_LONG).show();
                    }
                });
            }
        }
    });
}
```

#### SharedPreferences

##### 写数据

```java
SharedPreferences.Editor editor = getSharedPreferences("LoginInfo",MODE_PRIVATE).edit(); //LoginInfo即写入LoginInfo.xml
                       editor.putString("username",String.valueOf(usernamebox.getText()));
                       editor.putString("password",String.valueOf(passwordbox.getText()));
                        editor.putBoolean("isLogin",true);
                        editor.apply();
```



##### 读数据

```java
SharedPreferences preferences = getSharedPreferences("LoginInfo",MODE_PRIVATE);
boolean isLogin = preferences.getBoolean("isLogin",false);
```

#### 解决RecyclerView滚动嵌套的bug

```
recyclerView.setFocusableInTouchMode(false);
```

