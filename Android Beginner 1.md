# Tugas Praktikum 3: Android Beginner 1

## Kelompok 5:
1. Azfa Rahma Putra Susanto (L0324008)
2. Hammam Ibnu Adi'Abdillah (L0324015)
3. Indra Fata Azhari L0324017)

## Source Code yang digunakan:

###
1. activity_main.xml:
   ~~~xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:gravity="center_horizontal"
    android:padding="16dp"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@drawable/foto_kopiku"
    android:backgroundTintMode="multiply">


      <TextView
        android:text="Selamat Datang di "
        android:textSize="28sp"
        android:textStyle="bold"
        android:textColor="@color/white"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="80dp"/>

      <TextView
        android:text="Jospar Josgenk Coffee"
        android:textSize="28sp"
        android:textStyle="bold"
        android:textColor="@color/white"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="200dp"/>

      <TextView
        android:text="Tempat terbaik lu buat ngopi, rebahan, dan pura-pura produktif. Kadang kita butuh kopi bukan karena ngantuk, tapi karena hidup lagi banyak plot twist. Santai aja, duduk, nikmati kopi, dan biarkan kafein yang bekerja. Chill Brou"
        android:textSize="15sp"
        android:textColor="@color/white"
        android:background="@drawable/bg_text"
        android:gravity="center"
        android:textAlignment="center"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="12dp"
        android:layout_marginBottom="70dp"/>

      <Button
        android:id="@+id/btnProfile"
        android:text="Go To Profile Owners"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="8dp"
        android:layout_marginBottom="16dp"/>

      <Button
        android:id="@+id/btnGithub"
        android:text="Go To JJ Github"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="8dp"
        android:layout_marginBottom="16dp"/>

   </LinearLayout>


2. activity_profile.xml:
   ~~~xml
   <?xml version="1.0" encoding="utf-8"?>
   <LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="16dp"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@drawable/foto_kopiku"
    android:backgroundTintMode="multiply">

      <TextView
        android:id="@+id/view_tree_view_model_store_owner"
        android:text="The Owners"
        android:textColor="@color/white"
        android:background="@drawable/bg_text"
        android:layout_marginBottom="10dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

      <androidx.cardview.widget.CardView
        android:layout_width="190dp"
        android:layout_height="300dp"
        android:layout_marginBottom="16dp"
        app:cardCornerRadius="60dp"
        app:cardElevation="4dp">

        <ImageView
            android:layout_width="match_parent"
            android:layout_height="332dp"
            android:scaleType="centerCrop"
            android:src="@drawable/ama_hammam_fata" />
      </androidx.cardview.widget.CardView>

      <TextView
        android:id="@+id/tvNim"
        android:text="NIM: L0324008, L0324015, L0324017"
        android:textColor="@color/white"
        android:gravity="center"
        android:background="@drawable/bg_text"
        android:layout_marginBottom="2dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

      <TextView
        android:id="@+id/tvNama"
        android:text="Nama: Azfa Rahma, Indra Fata, Hammam Ibnu"
        android:textColor="@color/white"
        android:gravity="center"
        android:background="@drawable/bg_text"
        android:layout_marginBottom="2dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

      <TextView
        android:id="@+id/tvJurusan"
        android:text="Jurusan: Informatika (2024)"
        android:textColor="@color/white"
        android:gravity="center"
        android:background="@drawable/bg_text"
        android:layout_marginBottom="2dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

      <TextView
        android:id="@+id/tvDeskripsi"
        android:text="Para Pemburu MBG"
        android:textColor="@color/white"
        android:gravity="center"
        android:background="@drawable/bg_text"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>

      <Button
        android:id="@+id/btnShare"
        android:text="Share"
        android:layout_marginTop="40dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

   </LinearLayout>


3. circle_bg.xml
   ~~~xml
   <?xml version="1.0" encoding="utf-8"?>
    <shape xmlns:android="http://schemas.android.com/apk/res/android"
       android:shape="oval">

       <solid android:color="#FFFFFF"/>

   </shape>
   
4. AndroidManifest.xml
   ~~~xml
   <?xml version="1.0" encoding="utf-8"?>
    <manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

      <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.IntentApp">
        <activity android:name=".ProfileActivity"/>
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:label="@string/app_name"
            android:theme="@style/Theme.IntentApp">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
      </application>

   </manifest>

5. MainActivity.kt
   ~~~kt
   package com.example.intentapp
   
   import android.R.attr.button
   import android.content.Intent
   import android.net.Uri
   import android.os.Bundle
   import android.widget.Button
   import androidx.appcompat.app.AppCompatActivity

   class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val btnProfile = findViewById<Button>(R.id.btnProfile)
        val btnGithub = findViewById<Button>(R.id.btnGithub)

        // Explicit Intent → pindah ke Profile
        btnProfile.setOnClickListener {
            val intent = Intent(this, ProfileActivity::class.java)
            startActivity(intent)
        }

        // Implicit Intent → buka Github
        btnGithub.setOnClickListener {
            val url = "https://github.com/josparjosgenkcoffee01"
            val intent = Intent(Intent.ACTION_VIEW, Uri.parse(url))
            startActivity(intent)
        }
    }
   }

6. ProfileActivity.kt
   ~~~kt
   package com.example.intentapp

   import android.content.Intent
   import android.os.Bundle
   import android.widget.Button
   import androidx.appcompat.app.AppCompatActivity

   class ProfileActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_profile)

        val btnShare = findViewById<Button>(R.id.btnShare)

        btnShare.setOnClickListener {
            val data = """
                NIM: L0324008
                Nama: Azfa Rahma Putra Susanto
                Jurusan: Informatika
                Deskripsi: Mahasiswa Gagah
            """.trimIndent()

            val intent = Intent(Intent.ACTION_SEND)
            intent.type = "text/plain"
            intent.putExtra(Intent.EXTRA_TEXT, data)

            startActivity(Intent.createChooser(intent, "Share via"))
        }
    }
   }

7. build.gradle.kts (:app)
   ~~~kts
   plugins {
    alias(libs.plugins.android.application)
    alias(libs.plugins.kotlin.compose)
   }

   android {
      namespace = "com.example.intentapp"
      compileSdk {
          version = release(36) {
              minorApiLevel = 1
        }
   }

    defaultConfig {
        applicationId = "com.example.intentapp"
        minSdk = 24
        targetSdk = 36
        versionCode = 1
        versionName = "1.0"

        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            isMinifyEnabled = false
            proguardFiles(
                getDefaultProguardFile("proguard-android-optimize.txt"),
                "proguard-rules.pro"
            )
        }
    }
    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_11
        targetCompatibility = JavaVersion.VERSION_11
    }
    buildFeatures {
        compose = true
    }
   }

    dependencies {
      implementation("androidx.cardview:cardview:1.0.0")
      implementation(libs.androidx.core.ktx)
      implementation(libs.androidx.lifecycle.runtime.ktx)
      implementation(libs.androidx.activity.compose)
      implementation(platform(libs.androidx.compose.bom))
      implementation(libs.androidx.compose.ui)
      implementation(libs.androidx.compose.ui.graphics)
      implementation(libs.androidx.compose.ui.tooling.preview)
      implementation(libs.androidx.compose.material3)
      implementation(libs.androidx.appcompat)
      testImplementation(libs.junit)
      androidTestImplementation(libs.androidx.junit)
      androidTestImplementation(libs.androidx.espresso.core)
      androidTestImplementation(platform(libs.androidx.compose.bom))
      androidTestImplementation(libs.androidx.compose.ui.test.junit4)
      debugImplementation(libs.androidx.compose.ui.tooling)
      debugImplementation(libs.androidx.compose.ui.test.manifest)
    }
