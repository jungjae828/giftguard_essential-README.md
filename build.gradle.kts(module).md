// app/build.gradle.kts (모듈 수준)

plugins {
    alias(libs.plugins.android.application)
    alias(libs.plugins.kotlin.android)
    alias(libs.plugins.google.android.libraries.mapsplatform.secrets.gradle.plugin)

    // ⭐ 수정된 별칭으로 적용
    alias(libs.plugins.composecompiler)
}

android {
    namespace = "com.example.mygtpmap"
    compileSdk = 36

    defaultConfig {
        applicationId = "com.example.mygtpmap"
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
        sourceCompatibility = JavaVersion.VERSION_17
        targetCompatibility = JavaVersion.VERSION_17
    }

    // `kotlinOptions` 블록은 삭제되었습니다. (JVM Target 경고 해결)

    buildFeatures {
        viewBinding = true
        compose = true
    }
}

// ⭐ kotlin 블록은 android 블록과 같은 최상위 레벨에 위치해야 합니다.
kotlin {
    compilerOptions {
        // Kotlin 2.0+ 컴파일러 옵션 설정
        jvmTarget.set(org.jetbrains.kotlin.gradle.dsl.JvmTarget.JVM_17)
    }
}


dependencies {

    implementation(libs.androidx.core.ktx)
    implementation(libs.androidx.appcompat)
    implementation(libs.material)
    implementation(libs.play.services.maps)
    implementation(libs.androidx.constraintlayout)
    implementation(libs.androidx.lifecycle.runtime.ktx)
    implementation(libs.androidx.activity.compose)
    implementation(platform(libs.androidx.compose.bom))
    implementation(libs.androidx.compose.ui)
    implementation(libs.androidx.compose.ui.graphics)
    implementation(libs.androidx.compose.ui.tooling.preview)
    implementation(libs.androidx.compose.material3)
    testImplementation(libs.junit)
    androidTestImplementation(libs.androidx.junit)
    androidTestImplementation(libs.androidx.espresso.core)
    implementation("androidx.activity:activity-ktx:1.9.2")
    implementation("com.google.mlkit:text-recognition:16.0.0")


}
