# Itqan School Android App + WordPress API (v1.1.0)

এই সংস্করণে ডেমো লগইন বাদ দিয়ে WordPress REST API-ভিত্তিক লগইন ও অ্যাডমিনের শিক্ষার্থী অ্যাকাউন্ট তৈরির ব্যবস্থা যুক্ত হয়েছে।

## ১. WordPress প্লাগইন আপডেট
1. আগে সম্পূর্ণ WordPress backup নিন।
2. পুরোনো Itqan School API plugin deactivate করুন।
3. নতুন `ItqanSchool_WordPress_API_Plugin_v1.1.0.zip` আপলোড করে activate করুন। একই plugin folder replace করার অপশন থাকলে সেটিও ব্যবহার করতে পারেন।
4. `https://itqanschool.com/wp-json/itqan/v1/health` খুলে version 1.1.0 নিশ্চিত করুন।

## ২. অ্যাডমিনের প্রথম লগইন
Android app-এ বিদ্যমান WordPress Administrator username ও password দিয়ে লগইন করুন। অ্যাডমিন অ্যাকাউন্টে `manage_options` capability থাকতে হবে।

## ৩. শিক্ষার্থী তৈরি
Admin dashboard-এর “নতুন শিক্ষার্থী যুক্ত করুন” ফরমে নাম, শ্রেণি ও অভিভাবকের মোবাইল দিন। রোল/অভিভাবকের নাম ঐচ্ছিক। Student ID না দিলে API `ITS-YYYY-0001` ফরম্যাটে তৈরি করবে। Password না দিলে ১২ অক্ষরের অস্থায়ী পাসওয়ার্ড তৈরি হবে।

অ্যাকাউন্ট তৈরির পর দেখানো Student ID ও temporary password অভিভাবককে নিরাপদে দিন। শিক্ষার্থী ও অভিভাবক একই credentials ব্যবহার করবেন। পাসওয়ার্ড প্রথম লগইনের পর বদলানোর নির্দেশ দিন।

## ৪. Android APK তৈরি
Android Studio-তে `ItqanSchoolAndroid` ফোল্ডার Open করুন, Gradle Sync করুন, তারপর Build > Build Bundle(s) / APK(s) > Build APK(s)। APK: `app/build/outputs/apk/debug/app-debug.apk`। এই পরিবেশে APK compile করা হয়নি।

## ৫. API endpoints
- `GET /wp-json/itqan/v1/health`
- `POST /wp-json/itqan/v1/login` body: `{"student_id":"ITS-2026-0001","password":"..."}`
- `GET /wp-json/itqan/v1/me` Bearer token
- `GET /wp-json/itqan/v1/dashboard` Bearer token
- `GET /wp-json/itqan/v1/students` administrator Bearer token
- `POST /wp-json/itqan/v1/students` administrator Bearer token
- `PUT /wp-json/itqan/v1/students/{user_id}` administrator Bearer token
- `POST /wp-json/itqan/v1/students/{user_id}/reset-password` administrator Bearer token

Create student JSON example:
```json
{
  "name": "শিক্ষার্থীর নাম",
  "class": "Class 1",
  "roll": "12",
  "guardian_name": "অভিভাবকের নাম",
  "guardian_phone": "01XXXXXXXXX"
}
```

## নিরাপত্তা ও সীমাবদ্ধতা
- HTTPS ছাড়া login বন্ধ থাকবে।
- Student creation/list/update কেবল WordPress administrator করতে পারবেন।
- Student account-এ WordPress-এর hashed password ব্যবহার হয়; plaintext password কেবল create/reset response-এ একবার ফেরত আসে।
- Login rate-limit IP-ভিত্তিক।
- App-এর current build login, profile, notice, admin student create/list পর্যন্ত যুক্ত। Routine/results/attendance/homework/fees-এর পূর্ণ management module এখনো সম্পূর্ণ নয়।
- Production-এ ব্যবহারের আগে staging-এ dummy data দিয়ে পরীক্ষা, hosting backup, privacy policy/guardian consent এবং independent security review করুন।
- Administrator password অ্যাপে hardcode করবেন না। অ্যাডমিন নিজের WordPress credentials দিয়ে লগইন করবেন; student credentials আলাদা হবে।
