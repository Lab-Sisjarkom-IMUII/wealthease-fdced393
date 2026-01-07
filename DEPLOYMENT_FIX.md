# 🚀 Panduan Deploy WealthEase

## ✅ Perbaikan yang Sudah Dilakukan

### 1. **Path Alias TypeScript**
- ✅ Root `tsconfig.json`: Path alias diubah ke `"@/*": ["./frontend/*"]`
- ✅ Frontend `tsconfig.json`: Path alias tetap `"@/*": ["./*"]`

### 2. **Build Configuration**
- ✅ `package.json` (root): Build command ke frontend
- ✅ `imuii.json`: Config deploy dengan build command yang benar
- ✅ `vercel.json`: Ditambahkan untuk platform Vercel

### 3. **Security**
- ✅ `frontend/.env.local`: Dihapus `SUPABASE_SERVICE_ROLE_KEY` dan `JWT_SECRET`
- ⚠️ Kedua key tersebut hanya untuk backend

### 4. **Code Fixes**
- ✅ `frontend/app/dashboard/page.tsx`: Duplikasi `totalExpense` dihapus
- ✅ `frontend/next.config.js`: Turbopack dinonaktifkan, webpack digunakan

---

## 📋 Environment Variables

### Frontend (`.env.local`)
```bash
NEXT_PUBLIC_API_URL=http://localhost:5000
NEXT_PUBLIC_SUPABASE_URL=https://bqmvorrxeziuyfjhqenv.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

### Backend (`.env`)
```bash
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
JWT_SECRET=f35bbcbb94f25447e780a5b430c4944383fbcd081dc492a04ff3027ccd15906a...
FRONTEND_URL=http://localhost:3000
BACKEND_URL=http://localhost:5000
PORT=5000
SUPABASE_URL=https://bqmvorrxeziuyfjhqenv.supabase.co
SUPABASE_SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
OPENAI_API_KEY=your-openai-api-key
```

---

## 🌐 Deploy ke IMUII Platform

### Step 1: Commit & Push
```bash
git add .
git commit -m "fix: build configuration and TypeScript errors"
git push origin main
```

### Step 2: Deploy
Platform IMUII akan otomatis:
1. Menjalankan `cd frontend && npm install`
2. Menjalankan `cd frontend && npm run build`
3. Deploy dari `frontend/.next`

### Step 3: Environment Variables di Platform
Pastikan set di dashboard platform:
- `NEXT_PUBLIC_API_URL` → URL backend Anda
- `NEXT_PUBLIC_SUPABASE_URL` → `https://bqmvorrxeziuyfjhqenv.supabase.co`
- `NEXT_PUBLIC_SUPABASE_ANON_KEY` → Anon key dari Supabase

---

## 🔧 Deploy ke Vercel (Opsional)

### Via Vercel CLI
```bash
npm i -g vercel
vercel --prod
```

### Via Vercel Dashboard
1. Import repository dari GitHub
2. **Root Directory**: `frontend`
3. **Framework Preset**: Next.js
4. **Build Command**: `npm run build`
5. **Output Directory**: `.next`
6. Set environment variables di dashboard

---

## 🐛 Troubleshooting

### Error: Module not found
```bash
cd frontend
rm -rf .next node_modules
npm install
npm run build
```

### Error: TypeScript compilation failed
- Pastikan `frontend/tsconfig.json` memiliki path alias yang benar
- Check apakah semua import menggunakan `@/` untuk absolute imports

### Warning: themeColor metadata
⚠️ Ini hanya warning, bukan error. Build tetap berhasil.
Untuk fix (opsional), pindahkan `themeColor` dari metadata ke viewport export.

---

## 📊 Build Status
✅ **Build Successful** (tested locally)
✅ **TypeScript Compilation**: Passed
✅ **All Routes Generated**: 11 pages
⚠️ **Warnings**: themeColor metadata (tidak mempengaruhi deploy)

---

## 📝 Catatan Penting

1. **API URL Production**: Ganti `NEXT_PUBLIC_API_URL` dengan URL backend production
2. **Google OAuth**: Set redirect URI di Google Console sesuai domain production
3. **CORS**: Backend harus allow origin dari domain frontend production
4. **Database**: Pastikan Supabase RLS policy sudah benar

---

## 🎯 Next Steps

1. ✅ Build lokal berhasil
2. 🔄 Commit & push ke repository
3. 🌐 Deploy ke platform (IMUII/Vercel)
4. ⚙️ Set environment variables di platform
5. 🧪 Test di production URL
