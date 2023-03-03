# WebView No Internet

### Add raw Directory and keep Lottie File


## XML Design :

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".AlQuran"
    android:orientation="vertical"
    >

    <WebView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/webView"
        />

    <LinearLayout
        android:id="@+id/layNonet"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:visibility="gone"
        >

        <include
            layout="@layout/no_internet"
            />

    </LinearLayout>


</LinearLayout>
```



## Java :

```
import androidx.appcompat.app.ActionBar;
import androidx.appcompat.app.AppCompatActivity;

import android.content.Context;
import android.graphics.Bitmap;
import android.graphics.BitmapFactory;
import android.net.ConnectivityManager;
import android.os.Build;
import android.os.Bundle;
import android.view.View;
import android.webkit.WebChromeClient;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;
import android.widget.FrameLayout;
import android.widget.LinearLayout;

import com.airbnb.lottie.LottieAnimationView;

public class AlQuran extends AppCompatActivity {

    WebView webView;
    LinearLayout layNonet;

    String USER_AGENT_ = "Mozilla/5.0 (Linux; Android 4.1.1; Galaxy Nexus Build/JRO03C) AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.166 Mobile Safari/535.19";
    public static String WEBSITE_LINK = "";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.al_quran);

        ActionBar actionBar = getSupportActionBar();
        actionBar.setTitle("আল-কুরআন");
        actionBar.setDisplayShowHomeEnabled(true);
        actionBar.setDisplayHomeAsUpEnabled(true);
        // ---------- Tool Bar -----------


        layNonet = findViewById(R.id.layNonet);


        // Enabling some setting so that browser can work properly
        webView.getSettings().setUserAgentString(USER_AGENT_);
        webView.getSettings().setLoadsImagesAutomatically(true);
        webView.getSettings().setJavaScriptEnabled(true);
        webView.getSettings().setLoadWithOverviewMode(true);
        webView.getSettings().setUseWideViewPort(true);


        //-------------------new setting
        webView.getSettings().setBlockNetworkLoads (false);
        webView.getSettings().setMediaPlaybackRequiresUserGesture(false);
        webView.getSettings().setDomStorageEnabled(true);

        if (Build.VERSION.SDK_INT >= 19) {
            webView.getSettings().setCacheMode(WebSettings.LOAD_CACHE_ELSE_NETWORK);
        }

        webView.loadUrl(WEBSITE_LINK);




        if(!isNetworkAvailable(AlQuran.this)){
            webView.setVisibility(View.GONE);
            layNonet.setVisibility(View.VISIBLE);
        }else{
            webView.setVisibility(View.VISIBLE);
            layNonet.setVisibility(View.GONE);
        }





    } // onCreate Ends here  >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>


    public static boolean isNetworkAvailable(Context context) {
        return ((ConnectivityManager) context
                .getSystemService(Context.CONNECTIVITY_SERVICE))
                .getActiveNetworkInfo() != null;
    }


}
```

## If you add Progressbar then
## XML :

```

    <com.airbnb.lottie.LottieAnimationView
        android:id="@+id/prograssbar"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:scaleType="centerInside"
        app:lottie_autoPlay="true"
        app:lottie_loop="true"
        app:lottie_rawRes="@raw/pdf_loading"
        app:lottie_repeatMode="restart"
        android:layout_marginTop="12dp"
        />

```
## webView is Gone


# Java :
```

LottieAnimationView prograssbar;
prograssbar = findViewById(R.id.prograssbar);



webView.setWebViewClient(new WebViewClient() {
            @Override
            public void onPageFinished(WebView view, String url) {
                // If the WebView has finished loading, set the textview to gone
                prograssbar.setVisibility(View.GONE);
                webView.setVisibility(View.VISIBLE);
            }
        });

        // If the WebView is still loading, set the progressbar to visible
        if (webView.getProgress() < 100) {
            prograssbar.setVisibility(View.VISIBLE);
            webView.setVisibility(View.GONE);
        } else {
            prograssbar.setVisibility(View.GONE);
            webView.setVisibility(View.VISIBLE);
        }
        
```




### Power By INNOVATIVE PROGRAMMER ❤️

