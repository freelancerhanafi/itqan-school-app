# APK তৈরি করার সহজ পদ্ধতি (GitHub Actions)

এই প্রজেক্টে `.github/workflows/build-apk.yml` যোগ করা হয়েছে। GitHub Actions দিয়ে APK তৈরি করা যাবে।

1. GitHub-এ একটি private repository তৈরি করুন।
2. এই ZIP-এর ভেতরের `ItqanSchoolAndroid` ফোল্ডারের সব ফাইল repository-তে upload করুন (root-এ `.github`, `app`, `build.gradle`, `settings.gradle` থাকবে)।
3. GitHub repository-র **Actions** ট্যাবে যান।
4. **Build Itqan School APK** workflow নির্বাচন করে **Run workflow** চাপুন।
5. কাজ শেষ হলে workflow run-এর নিচে **Artifacts** থেকে `Itqan-School-debug-apk` ডাউনলোড করুন।
6. ZIP extract করে `app-debug.apk` Android ফোনে পাঠিয়ে ইনস্টল করুন। প্রয়োজনে Android-এ ওই ফাইল/ব্রাউজারের জন্য “Install unknown apps” অনুমতি দিন।

নোট: এই পরিবেশে Android SDK/Gradle নেই, তাই এখানে APK নিজে compile করা যায়নি। GitHub Actions-এ build সফল না হওয়া পর্যন্ত APK-কে পরীক্ষিত বলা যাবে না। এটি debug APK; Play Store release-এর জন্য আলাদা signed release build প্রয়োজন।
