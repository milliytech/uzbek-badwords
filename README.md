# 🟡Yomon So‘zlar Arxivi - Senzura Qiluvchi Platforma

Yomon So‘zlar Arxivi, o'zbek tilidagi nojo'ya so'zlarni senzuradan o'tkazish uchun mo'ljallangan platforma.

### Disclaimer⚠️
🔞Bu loyihada ko'plab haqoratli so'zlar mavjud bo'lishi mumkin. Ushbu so'zlar faqat o'zbek tilidagi nojo'ya so'zlar ro'yxatidan olingan. Ushbu so'zlar faqat ma'lumotlar olish maqsadida ishlatiladi va ularni ishlatishdan kelib chiqadigan huquqiy javobgarlik sizga tegishli bo'lishi mumkin.
18 yoshdan kichiklar uchun bu loyiha tavsiya etilmaydi.

## Maqsad
Bu loyiha o'zbek tilidagi nojo'ya so'zlarni aniqlash va ularni platformadan olib tashlash maqsadida yaratilgan.

## Resurslar
- [MilliyTech](https://milliytech.uz) - MilliyTech sayti
- [Telegram](https://t.me/jakhangir_blog) - Telegram kanal
- [Bad](https://bad.milliytech.uz) - Yomon so'zlar platformasi
- [Bad API](https://api.badwords.milliytech.uz/api/v1/badword/) - Yomon so'zlar platformasi API

**CSV, JSON, XLSX** formatlarida yomon so'zlar ro'yxati:

| No   | So'zlar                          | Turi    | Holati  |
|------|----------------------------------|---------|---------|
| 1    | [CSV](resources/bad_words.csv)   | CSV     | ✅      |
| 2    | [JSON](resources/bad_words.json) | JSON    | ✅      |
| 3    | [XLSX](resources/bad_words.xlsx) | XLSX    | ✅      |



## Qanday foydalanish
Loyihani ishlatish uchun quyidagi ko'rsatmalarga amal qiling:

1. **Yuklab oling**: Loyiha fayllarini yuklab oling yoki klon qiling.
2. **O'rnating**: Zaruriy bog'lamalarni o'rnating va loyiha fayllarini tayyorlang.
3. **Ishga tushiring**: Loyihani ishga tushiring va nojo'ya so'zlarni aniqlashni boshlang.

## Hissa qo'shish
Agar loyihaga hissa qo'shmoqchi bo'lsangiz, quyidagi qadamlarni bajaring:

1. **Fork**: Loyiha repositorysini fork qiling.
2. **Branch**: Yangi branch yarating (`git checkout -b feature-branch`).
3. **O'zgarishlar**: Zaruriy o'zgarishlarni kiriting va commit qiling (`git commit -m 'Add some feature'`).
4. **Pull Request**: Pull request yarating va loyihaga qo'shing.
5. **So'z qo'shish**: https://bad.milliytech.uz/ saytiga kirib, so'z qo'shing va u so'z chindan ham yomon so'z deb qoshilsa tez orada platformaga qo'shiladi.

## Litsenziya
Bu loyiha [MIT Litsenziyasi](LICENSE) ostida tarqatiladi.

## Aloqa
Agar sizda savollar yoki takliflar bo'lsa, iltimos, [Telegram](https://t.me/ja_khan_gir) orqali bog'laning.

![image](assets/bad.webp)

---

**Diqqat**: Bu loyiha hali rivojlanish bosqichida va ba'zi funksiyalar to'liq ishga tushirilmagan bo'lishi mumkin.


# API Documentation

## Endpoints

### BASE_URL = `https://api.badwords.milliytech.uz`

### 1. List Bad Words

#### `GET /api/v1/badword/`

**Description:** Yomon so'zlar ro'yxatini olish.

**Query Parameters:**
- `sort` (optional): Tartibni belgilash uchun so'z. Mavjud qiymatlar: [`word`, `-word`, `created_at`, `-created_at`, `updated_at`, `-updated_at`, `id`, `-id`].
- `search` (optional): Qidiruv so'zi. Yomon so'zlarni qidirish uchun ishlatiladi.
- `page` (optional): Sahifa raqami. Paginatsiya uchun ishlatiladi.
- `page_size` (optional): Sahifadagi elementlar soni. Paginatsiya uchun ishlatiladi.

**Response:**
- `200 OK`: Muvaffaqiyatli so'rov. Yomon so'zlar ro'yxatini qaytaradi.
- `400 Bad Request`: Xato so'rov, agar `sort` yoki `search` parametrlari noto'g'ri bo'lsa.

**Example Response:**
```json
{
  "success": true,
  "message": "Data fetched successfully.",
  "links": {
    "next": "https://api.badwords.milliytech.uz/api/v1/badword/?page=2",
    "previous": null
  },
  "total_items": 98,
  "total_pages": 20,
  "page_size": 5,
  "current_page": 1,
  "data": [
    {
      "id": 77,
      "word": "Word",
      "created_at": "2025-03-31T22:54:48.782700+05:00",
      "updated_at": "2025-04-01T12:09:05.015195+05:00"
    }
]
}
```

### 2. Check Bad Word

#### `POST /api/v1/badword/check/`

**Description:** Yomon so'zlarni gaplardan tekshirish.

**Query Parameters:**
- `text` (required): Yomon so'zlarni tekshirish uchun matn. Maxsus belgilarni o'z ichiga olishi mumkin.

**Response:**
- `200 OK`: Muvaffaqiyatli so'rov. Yomon so'zlar ro'yxatini qaytaradi.
- `400 Bad Request`: Xato so'rov, agar `text` parametri noto'g'ri bo'lsa.
- `500 Internal Server Error`: Serverda xato yuz bersa.

**Example Response:**
URL: `https://api.badwords.milliytech.uz/api/v1/badword/check/?text=<your whole sentence>`
```json
{
    "success": true,
    "message": "Bad words found",
    "data": [
        {
            "text": "Your bad message word1, word2",
            "bad_words": [
                "word1",
                "word2"
            ],
            "bad_word_count": 2
        }
    ]
}
```




