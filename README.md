

# 1. history install setup 

```bash

ASUS TUF GAMING A15@ASUSTUF-ALVINZP MINGW64 ~/Desktop/Project/NODEJS_TS (main)
$ npm install           # install deps dari root (opsional kalau ada)
cd frontend
npm install           # install frontend (Next.js + Tailwind)
cd ../backend
npm install           # install backend (Express/Node)
cd ..

added 18 packages, and audited 19 packages in 5s

7 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
npm notice
npm notice New major version of npm available! 9.9.4 -> 11.4.2
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.4.2
npm notice Run npm install -g npm@11.4.2 to update!
npm notice

added 169 packages, and audited 170 packages in 42s

40 packages are looking for funding
  run `npm fund` for details

1 critical severity vulnerability

To address all issues, run:
  npm audit fix --force

Run `npm audit` for details.

added 130 packages, and audited 131 packages in 2s

20 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities

ASUS TUF GAMING A15@ASUSTUF-ALVINZP MINGW64 ~/Desktop/Project/NODEJS_TS (main)
$

ASUS TUF GAMING A15@ASUSTUF-ALVINZP MINGW64 ~/Desktop/Project/NODEJS_TS (main)
$ npm install -g npm@11.4.2

removed 80 packages, and changed 109 packages in 7s

25 packages are looking for funding
  run `npm fund` for details

ASUS TUF GAMING A15@ASUSTUF-ALVINZP MINGW64 ~/Desktop/Project/NODEJS_TS (main)
$
```



# 2. buat file .env dir di backend

```bash
DB_USER=postgres
DB_PASSWORD=postgres
DB_HOST=localhost
DB_PORT=5432
DB_DATABASE=fp_mbd_backend
DB_SSL_MODE=disable
```



# 3. run backend

```bash
cd backend
node src/server.js
```

# 4. history run backend Express JS

```bash
ASUS TUF GAMING A15@ASUSTUF-ALVINZP MINGW64 ~/Desktop/Project/NODEJS_TS (main)
$ ls
backend/  frontend/  node_modules/  package.json  package-lock.json  README.md

ASUS TUF GAMING A15@ASUSTUF-ALVINZP MINGW64 ~/Desktop/Project/NODEJS_TS (main)
$ cd backend
node src/server.js
Server berjalan di port 5000
```

# 5. run frontend

```bash
cd frontend
npm run dev
```

# 6. history run frontend TypeScript

```bash

ASUS TUF GAMING A15@ASUSTUF-ALVINZP MINGW64 ~/Desktop/Project/NODEJS_TS (main)
$ cd frontend
npm run dev

> myits-mental-health-frontend@0.1.0 dev
> next dev

  ▲ Next.js 14.2.4
  - Local:        http://localhost:3000

 ✓ Starting...
 ✓ Ready in 2.8s
 ○ Compiling / ...
 ✓ Compiled / in 7.2s (713 modules)
 GET / 200 in 7793ms
 ✓ Compiled in 606ms (324 modules)
 ○ Compiling /auth/login ...
 ✓ Compiled /auth/login in 3.9s (700 modules)


```



# 7. Database in terminal 

```bash

ASUS TUF GAMING A15@ASUSTUF-ALVINZP MINGW64 ~
$ psql -U postgres -d fp_mbd_backend
psql (17.4)
WARNING: Console code page (437) differs from Windows code page (1252)
         8-bit characters might not work correctly. See psql reference
         page "Notes for Windows users" for details.
Type "help" for help.

fp_mbd_backend=# \dt
             List of relations
 Schema |      Name      | Type  |  Owner
--------+----------------+-------+----------
 public | User           | table | postgres
 public | admin          | table | postgres
 public | konselor       | table | postgres
 public | konselor_topik | table | postgres
 public | mahasiswa      | table | postgres
 public | sesi           | table | postgres
 public | topik          | table | postgres
(7 rows)


fp_mbd_backend=# \d "User"
                        Table "public.User"
  Column  |          Type          | Collation | Nullable | Default
----------+------------------------+-----------+----------+---------
 user_id  | character(4)           |           | not null |
 username | character varying(50)  |           | not null |
 password | character varying(100) |           | not null |
 role     | character varying(10)  |           | not null |
Indexes:
    "User_pkey" PRIMARY KEY, btree (user_id)
    "User_username_key" UNIQUE CONSTRAINT, btree (username)
Referenced by:
    TABLE "admin" CONSTRAINT "fk_admin_user" FOREIGN KEY (user_user_id) REFERENCES "User"(u
ser_id) ON UPDATE CASCADE ON DELETE CASCADE
    TABLE "konselor" CONSTRAINT "fk_konselor_user" FOREIGN KEY (user_user_id) REFERENCES "U
ser"(user_id) ON UPDATE CASCADE ON DELETE CASCADE
    TABLE "mahasiswa" CONSTRAINT "fk_mahasiswa_user" FOREIGN KEY (user_user_id) REFERENCES
"User"(user_id) ON UPDATE CASCADE ON DELETE CASCADE


fp_mbd_backend=# \d admin
                          Table "public.admin"
    Column    |          Type          | Collation | Nullable | Default
--------------+------------------------+-----------+----------+---------
 admin_id     | character(4)           |           | not null |
 nama         | character varying(100) |           | not null |
 user_user_id | character(4)           |           | not null |
Indexes:
    "admin_pkey" PRIMARY KEY, btree (admin_id)
    "admin_user_user_id_key" UNIQUE CONSTRAINT, btree (user_user_id)
Foreign-key constraints:
    "fk_admin_user" FOREIGN KEY (user_user_id) REFERENCES "User"(user_id) ON UPDATE CASCADE
 ON DELETE CASCADE
Referenced by:
    TABLE "sesi" CONSTRAINT "fk_sesi_admin" FOREIGN KEY (admin_admin_id) REFERENCES admin(a
dmin_id) ON UPDATE CASCADE ON DELETE RESTRICT
    TABLE "topik" CONSTRAINT "fk_topik_admin" FOREIGN KEY (admin_admin_id) REFERENCES admin
(admin_id) ON UPDATE CASCADE ON DELETE RESTRICT


fp_mbd_backend=# \d konselor
                        Table "public.konselor"
    Column    |          Type          | Collation | Nullable | Default
--------------+------------------------+-----------+----------+---------
 nik          | character(16)          |           | not null |
 nama         | character varying(100) |           | not null |
 spesialisasi | character varying(100) |           | not null |
 kontak       | character varying(15)  |           | not null |
 user_user_id | character(4)           |           | not null |
Indexes:
    "konselor_pkey" PRIMARY KEY, btree (nik)
    "konselor_user_user_id_key" UNIQUE CONSTRAINT, btree (user_user_id)
Foreign-key constraints:
    "fk_konselor_user" FOREIGN KEY (user_user_id) REFERENCES "User"(user_id) ON UPDATE CASC
ADE ON DELETE CASCADE
Referenced by:
    TABLE "konselor_topik" CONSTRAINT "fk_konselor_topik_konselor" FOREIGN KEY (konselor_ni
k) REFERENCES konselor(nik) ON UPDATE CASCADE ON DELETE CASCADE
    TABLE "sesi" CONSTRAINT "fk_sesi_konselor" FOREIGN KEY (konselor_nik) REFERENCES konsel
or(nik) ON UPDATE CASCADE ON DELETE RESTRICT


fp_mbd_backend=# \d konselor_topik
                  Table "public.konselor_topik"
     Column     |     Type      | Collation | Nullable | Default
----------------+---------------+-----------+----------+---------
 konselor_nik   | character(16) |           | not null |
 topik_topik_id | character(4)  |           | not null |
Indexes:
    "konselor_topik_pkey" PRIMARY KEY, btree (konselor_nik, topik_topik_id)
Foreign-key constraints:
    "fk_konselor_topik_konselor" FOREIGN KEY (konselor_nik) REFERENCES konselor(nik) ON UPD
ATE CASCADE ON DELETE CASCADE
    "fk_konselor_topik_topik" FOREIGN KEY (topik_topik_id) REFERENCES topik(topik_id) ON UP
DATE CASCADE ON DELETE CASCADE


fp_mbd_backend=# \d mahasiswa
                        Table "public.mahasiswa"
    Column    |          Type          | Collation | Nullable | Default
--------------+------------------------+-----------+----------+---------
 nrp          | character(10)          |           | not null |
 nama         | character varying(100) |           | not null |
 departemen   | character varying(30)  |           | not null |
 kontak       | character varying(15)  |           | not null |
 user_user_id | character(4)           |           | not null |
Indexes:
    "mahasiswa_pkey" PRIMARY KEY, btree (nrp)
    "mahasiswa_user_user_id_key" UNIQUE CONSTRAINT, btree (user_user_id)
Foreign-key constraints:
    "fk_mahasiswa_user" FOREIGN KEY (user_user_id) REFERENCES "User"(user_id) ON UPDATE CAS
CADE ON DELETE CASCADE
Referenced by:
    TABLE "sesi" CONSTRAINT "fk_sesi_mahasiswa" FOREIGN KEY (mahasiswa_nrp) REFERENCES mahasiswa(nrp) ON UPDATE CASCADE ON DELETE RESTRICT


fp_mbd_backend=# \d sesi
                              Table "public.sesi"
     Column     |            Type             | Collation | Nullable | Default
----------------+-----------------------------+-----------+----------+---------
 sesi_id        | character(4)                |           | not null |
 tanggal        | timestamp without time zone |           | not null |
 status         | character varying(20)       |           | not null |
 catatan        | text                        |           |          |
 mahasiswa_nrp  | character(10)               |           | not null |
 konselor_nik   | character(16)               |           | not null |
 admin_admin_id | character(4)                |           | not null |
 topik_topik_id | character(4)                |           | not null |
Indexes:
    "sesi_pkey" PRIMARY KEY, btree (sesi_id)
Foreign-key constraints:
    "fk_sesi_admin" FOREIGN KEY (admin_admin_id) REFERENCES admin(admin_id) ON UPDATE CASCADE ON DELETE RESTRICT
    "fk_sesi_konselor" FOREIGN KEY (konselor_nik) REFERENCES konselor(nik) ON UPDATE CASCADE ON DELETE RESTRICT
    "fk_sesi_mahasiswa" FOREIGN KEY (mahasiswa_nrp) REFERENCES mahasiswa(nrp) ON UPDATE CASCADE ON DELETE RESTRICT
    "fk_sesi_topik" FOREIGN KEY (topik_topik_id) REFERENCES topik(topik_id) ON UPDATE CASCADE ON DELETE RESTRICT


fp_mbd_backend=# \d topik
                           Table "public.topik"
     Column     |          Type          | Collation | Nullable | Default
----------------+------------------------+-----------+----------+---------
 topik_id       | character(4)           |           | not null |
 topik_nama     | character varying(100) |           | not null |
 admin_admin_id | character(4)           |           | not null |
Indexes:
    "topik_pkey" PRIMARY KEY, btree (topik_id)
Foreign-key constraints:
    "fk_topik_admin" FOREIGN KEY (admin_admin_id) REFERENCES admin(admin_id) ON UPDATE CASCADE ON DELETE RESTRICT
Referenced by:
    TABLE "konselor_topik" CONSTRAINT "fk_konselor_topik_topik" FOREIGN KEY (topik_topik_id) REFERENCES topik(topik_id) ON UPDATE CASCADE ON DELETE CASCADE
    TABLE "sesi" CONSTRAINT "fk_sesi_topik" FOREIGN KEY (topik_topik_id) REFERENCES topik(topik_id) ON UPDATE CASCADE ON DELETE RESTRICT


fp_mbd_backend=# SELECT * FROM "User";
 user_id |    username     |          password           |   role
---------+-----------------+-----------------------------+-----------
 U001    | admin_eko       | hashed_password_placeholder | admin
 U002    | admin_sari      | hashed_password_placeholder | admin
 U003    | admin_jaya      | hashed_password_placeholder | admin
 U004    | admin_rini      | hashed_password_placeholder | admin
 U005    | admin_putra     | hashed_password_placeholder | admin
 U006    | konselor_budi   | hashed_password_placeholder | konselor
 U007    | konselor_dewi   | hashed_password_placeholder | konselor
 U008    | konselor_agung  | hashed_password_placeholder | konselor
 U009    | konselor_fitri  | hashed_password_placeholder | konselor
 U010    | konselor_hendra | hashed_password_placeholder | konselor
 U011    | konselor_indah  | hashed_password_placeholder | konselor
 U012    | konselor_lukman | hashed_password_placeholder | konselor
 U013    | konselor_maya   | hashed_password_placeholder | konselor
 U014    | konselor_nanda  | hashed_password_placeholder | konselor
 U015    | konselor_olivia | hashed_password_placeholder | konselor
 U016    | mhs_adi         | hashed_password_placeholder | mahasiswa
 U017    | mhs_bella       | hashed_password_placeholder | mahasiswa
 U018    | mhs_chandra     | hashed_password_placeholder | mahasiswa
 U019    | mhs_diana       | hashed_password_placeholder | mahasiswa
 U020    | mhs_erwin       | hashed_password_placeholder | mahasiswa
 U021    | mhs_farah       | hashed_password_placeholder | mahasiswa
 U022    | mhs_ganjar      | hashed_password_placeholder | mahasiswa
 U023    | mhs_hana        | hashed_password_placeholder | mahasiswa
 U024    | mhs_ivan        | hashed_password_placeholder | mahasiswa
 U025    | mhs_jenny       | hashed_password_placeholder | mahasiswa
 U026    | mhs_kiki        | hashed_password_placeholder | mahasiswa
 U027    | mhs_leo         | hashed_password_placeholder | mahasiswa
 U028    | mhs_mona        | hashed_password_placeholder | mahasiswa
 U029    | mhs_nino        | hashed_password_placeholder | mahasiswa
 U030    | mhs_oscar       | hashed_password_placeholder | mahasiswa
 U031    | mhs_putri       | hashed_password_placeholder | mahasiswa
 U032    | mhs_qori        | hashed_password_placeholder | mahasiswa
 U033    | mhs_rama        | hashed_password_placeholder | mahasiswa
 U034    | mhs_sinta       | hashed_password_placeholder | mahasiswa
 U035    | mhs_toni        | hashed_password_placeholder | mahasiswa
 U036    | mhs_ulia        | hashed_password_placeholder | mahasiswa
 U037    | mhs_vino        | hashed_password_placeholder | mahasiswa
 U038    | mhs_wulan       | hashed_password_placeholder | mahasiswa
 U039    | mhs_xena        | hashed_password_placeholder | mahasiswa
 U040    | mhs_yuda        | hashed_password_placeholder | mahasiswa
 U041    | mhs_zara        | hashed_password_placeholder | mahasiswa
 U042    | mhs_angga       | hashed_password_placeholder | mahasiswa
 U043    | mhs_bima        | hashed_password_placeholder | mahasiswa
 U044    | mhs_citra       | hashed_password_placeholder | mahasiswa
 U045    | mhs_doni        | hashed_password_placeholder | mahasiswa
 U046    | mhs_elsa        | hashed_password_placeholder | mahasiswa
 U047    | mhs_fajar       | hashed_password_placeholder | mahasiswa
 U048    | mhs_gina        | hashed_password_placeholder | mahasiswa
 U049    | mhs_hari        | hashed_password_placeholder | mahasiswa
 U050    | mhs_irma        | hashed_password_placeholder | mahasiswa
 U051    | mhs_jaka        | hashed_password_placeholder | mahasiswa
 U052    | mhs_karen       | hashed_password_placeholder | mahasiswa
 U053    | mhs_lisa        | hashed_password_placeholder | mahasiswa
 U054    | mhs_mira        | hashed_password_placeholder | mahasiswa
 U055    | mhs_nita        | hashed_password_placeholder | mahasiswa
(55 rows)


fp_mbd_backend=# SELECT * FROM admin;
 admin_id |      nama      | user_user_id
----------+----------------+--------------
 A001     | Eko Prasetyo   | U001
 A002     | Sari Hartati   | U002
 A003     | Jaya Wijaya    | U003
 A004     | Rini Anggraini | U004
 A005     | Putra Santoso  | U005
(5 rows)


fp_mbd_backend=# SELECT * FROM konselor;
       nik        |           nama           |         spesialisasi          |    kontak    | user_user_id
------------------+--------------------------+-------------------------------+--------------+--------------
 3578012345670001 | Dr. Budi Santoso, M.Psi. | Karir dan Pekerjaan           | 081234567890 | U006
 3578012345670002 | Dewi Lestari, S.Psi.     | Kesehatan Mental              | 081234567891 | U007
 3578012345670003 | Agung Nugroho, M.Psi.    | Masalah Akademik              | 081234567892 | U008
 3578012345670004 | Fitriani Hapsari, S.Psi. | Hubungan Interpersonal        | 081234567893 | U009
 3578012345670005 | Hendra Setiawan, M.Psi.  | Pengembangan Diri             | 081234567894 | U010
 3578012345670006 | Indah Permata, S.Psi.    | Manajemen Stres dan Kecemasan | 081234567895 | U011
 3578012345670007 | Lukman Hakim, M.Psi.     | Masalah Keluarga              | 081234567896 | U012
 3578012345670008 | Maya Sari, S.Psi.        | Karir dan Pekerjaan           | 081234567897 | U013
 3578012345670009 | Nanda Kusuma, M.Psi.     | Masalah Akademik              | 081234567898 | U014
 3578012345670010 | Olivia Rahma, S.Psi.     | Kesehatan Mental              | 081234567899 | U015
(10 rows)


fp_mbd_backend=# SELECT * FROM konselor_topik;
   konselor_nik   | topik_topik_id
------------------+----------------
 3578012345670001 | T004
 3578012345670001 | T005
 3578012345670001 | T014
 3578012345670002 | T007
 3578012345670002 | T015
 3578012345670002 | T016
 3578012345670003 | T002
 3578012345670003 | T003
 3578012345670003 | T019
 3578012345670004 | T006
 3578012345670004 | T011
 3578012345670004 | T017
 3578012345670005 | T008
 3578012345670005 | T009
 3578012345670005 | T018
 3578012345670006 | T001
 3578012345670006 | T007
 3578012345670006 | T020
 3578012345670007 | T012
 3578012345670007 | T006
 3578012345670008 | T004
 3578012345670008 | T005
 3578012345670008 | T014
 3578012345670009 | T002
 3578012345670009 | T013
 3578012345670009 | T019
 3578012345670010 | T007
 3578012345670010 | T016
 3578012345670010 | T020
(29 rows)


fp_mbd_backend=# SELECT * FROM mahasiswa;
    nrp     |      nama       |        departemen        |    kontak    | user_user_id
------------+-----------------+--------------------------+--------------+--------------
 5025211001 | Adi Nugraha     | Teknik Informatika       | 085712340001 | U016
 5025211002 | Bella Safira    | Sistem Informasi         | 085712340002 | U017
 5026211003 | Chandra Wijaya  | Manajemen Bisnis         | 085712340003 | U018
 5027211004 | Diana Putri     | Akuntansi                | 085712340004 | U019
 5025211005 | Erwin Prasetya  | Teknik Informatika       | 085712340005 | U020
 5028211006 | Farah Nabila    | Ilmu Komunikasi          | 085712340006 | U021
 5029211007 | Ganjar Aditama  | Desain Komunikasi Visual | 085712340007 | U022
 5030211008 | Hana Malika     | Teknik Elektro           | 085712340008 | U023
 5025211009 | Ivan Gunawan    | Teknik Informatika       | 085712340009 | U024
 5026211010 | Jenny Anggraini | Sistem Informasi         | 085712340010 | U025
 5027211011 | Kiki Maulana    | Manajemen Bisnis         | 085712340011 | U026
 5028211012 | Leo Firmansyah  | Ilmu Komunikasi          | 085712340012 | U027
 5029211013 | Mona Lestari    | Desain Komunikasi Visual | 085712340013 | U028
 5030211014 | Nino Setiawan   | Teknik Elektro           | 085712340014 | U029
 5025211015 | Oscar Haris     | Teknik Informatika       | 085712340015 | U030
 5026211016 | Putri Amelia    | Sistem Informasi         | 085712340016 | U031
 5027211017 | Qori Ramadhan   | Manajemen Bisnis         | 085712340017 | U032
 5028211018 | Rama Dhani      | Ilmu Komunikasi          | 085712340018 | U033
 5029211019 | Sinta Dewi      | Desain Komunikasi Visual | 085712340019 | U034
 5030211020 | Toni Saputra    | Teknik Elektro           | 085712340020 | U035
 5025211021 | Ulia Rahma      | Teknik Informatika       | 085712340021 | U036
 5026211022 | Vino Bastian    | Sistem Informasi         | 085712340022 | U037
 5027211023 | Wulan Sari      | Manajemen Bisnis         | 085712340023 | U038
 5028211024 | Xena Gabriella  | Ilmu Komunikasi          | 085712340024 | U039
 5029211025 | Yuda Pratama    | Desain Komunikasi Visual | 085712340025 | U040
 5030211026 | Zara Adhisty    | Teknik Elektro           | 085712340026 | U041
 5025211027 | Angga Yunanda   | Teknik Informatika       | 085712340027 | U042
 5026211028 | Bima Sakti      | Sistem Informasi         | 085712340028 | U043
 5027211029 | Citra Kirana    | Manajemen Bisnis         | 085712340029 | U044
 5028211030 | Doni Salmanan   | Ilmu Komunikasi          | 085712340030 | U045
 5029211031 | Elsa Japasal    | Desain Komunikasi Visual | 085712340031 | U046
 5030211032 | Fajar Alfian    | Teknik Elektro           | 085712340032 | U047
 5025211033 | Gina Meidina    | Teknik Informatika       | 085712340033 | U048
 5026211034 | Hari Santoso    | Sistem Informasi         | 085712340034 | U049
 5027211035 | Irma Suryani    | Manajemen Bisnis         | 085712340035 | U050
 5028211036 | Jaka Tarub      | Ilmu Komunikasi          | 085712340036 | U051
 5029211037 | Karenina        | Desain Komunikasi Visual | 085712340037 | U052
 5030211038 | Lisa Manoban    | Teknik Elektro           | 085712340038 | U053
 5025211039 | Mira Hayati     | Teknik Informatika       | 085712340039 | U054
 5026211040 | Nita Gunawan    | Sistem Informasi         | 085712340040 | U055
(40 rows)


fp_mbd_backend=# SELECT * FROM sesi;
 sesi_id |       tanggal       |   status    |                            catatan                            | mahasiswa_nrp |   konselor_nik   | admin_admin_id | topik_topik_id
---------+---------------------+-------------+---------------------------------------------------------------+---------------+------------------+----------------+----------------
 S001    | 2024-10-01 10:00:00 | Selesai     | Mahasiswa menunjukkan kemajuan dalam mengatasi prokrastinasi. | 5025211001    | 3578012345670003 | A001           | T002
 S002    | 2024-10-01 11:00:00 | Selesai     | Sesi awal untuk pembuatan CV.                                 | 5025211002    | 3578012345670001 | A002           | T005
 S003    | 2024-10-02 13:00:00 | Selesai     | Membahas teknik relaksasi untuk mengatasi cemas.              | 5026211003    | 3578012345670002 | A003           | T007
 S004    | 2024-10-02 14:00:00 | Dijadwalkan |                                                               | 5027211004    | 3578012345670004 | A004           | T006
 S005    | 2024-10-03 09:00:00 | Selesai     | Mahasiswa merasa lebih percaya diri.                          | 5025211005    | 3578012345670005 | A005           | T009
 S006    | 2024-10-03 10:00:00 | Dibatalkan  | Dibatalkan oleh mahasiswa.                                    | 5028211006    | 3578012345670006 | A001           | T001
 S007    | 2024-10-04 11:00:00 | Selesai     | Diskusi mengenai masalah keluarga yang mempengaruhi studi.    | 5029211007    | 3578012345670007 | A002           | T012
 S008    | 2024-10-04 13:00:00 | Selesai     | Follow-up sesi CV, portofolio sudah lebih baik.               | 5025211009    | 3578012345670008 | A003           | T005
 S009    | 2024-10-05 14:00:00 | Selesai     | Mahasiswa mulai menerapkan strategi belajar baru.             | 5026211010    | 3578012345670009 | A004           | T003
 S010    | 2024-10-05 15:00:00 | Selesai     | Latihan mindfulness.                                          | 5027211011    | 3578012345670010 | A005           | T020
 S011    | 2024-11-06 10:00:00 | Selesai     | Mahasiswa berhasil mengurangi waktu di media sosial.          | 5028211012    | 3578012345670002 | A001           | T015
 S012    | 2024-11-06 11:00:00 | Selesai     | Review CV untuk persiapan magang.                             | 5029211013    | 3578012345670001 | A002           | T005
 S013    | 2024-11-07 13:00:00 | Selesai     | Sesi lanjutan prokrastinasi, progres baik.                    | 5025211001    | 3578012345670003 | A003           | T002
 S014    | 2024-11-07 14:00:00 | Dijadwalkan |                                                               | 5030211014    | 3578012345670004 | A004           | T011
 S015    | 2024-11-08 09:00:00 | Selesai     | Diskusi tentang quarter-life crisis.                          | 5025211015    | 3578012345670005 | A005           | T008
 S016    | 2024-11-08 10:00:00 | Selesai     | Mengatasi stres menjelang UAS.                                | 5026211016    | 3578012345670006 | A001           | T001
 S017    | 2024-11-09 11:00:00 | Dibatalkan  | Konselor berhalangan.                                         | 5027211017    | 3578012345670007 | A002           | T012
 S018    | 2024-11-09 13:00:00 | Selesai     | Simulasi wawancara kerja.                                     | 5028211018    | 3578012345670008 | A003           | T004
 S019    | 2024-11-10 14:00:00 | Selesai     | Membahas burnout akademik dan solusinya.                      | 5029211019    | 3578012345670009 | A004           | T013
 S020    | 2024-11-10 15:00:00 | Selesai     | Membantu mahasiswa mengatasi rasa kesepian.                   | 5030211020    | 3578012345670010 | A005           | T016
 S021    | 2025-01-11 10:00:00 | Selesai     | Evaluasi strategi belajar, IPK meningkat.                     | 5025211021    | 3578012345670003 | A001           | T003
 S022    | 2025-01-11 11:00:00 | Selesai     | Membahas pilihan karir setelah lulus.                         | 5026211022    | 3578012345670001 | A002           | T014
 S023    | 2025-01-12 13:00:00 | Selesai     | Latihan pernapasan untuk mengatasi panik.                     | 5027211023    | 3578012345670002 | A003           | T007
 S024    | 2025-01-12 14:00:00 | Dijadwalkan |                                                               | 5028211024    | 3578012345670004 | A004           | T017
 S025    | 2025-01-13 09:00:00 | Selesai     | Membangun kebiasaan membaca buku.                             | 5029211025    | 3578012345670005 | A005           | T018
 S026    | 2025-01-13 10:00:00 | Selesai     | Diskusi manajemen stres.                                      | 5030211026    | 3578012345670006 | A001           | T001
 S027    | 2025-01-14 11:00:00 | Selesai     | Menangani konflik dalam keluarga.                             | 5025211027    | 3578012345670007 | A002           | T012
 S028    | 2025-01-14 13:00:00 | Selesai     | Praktik wawancara lanjutan.                                   | 5026211028    | 3578012345670008 | A003           | T004
 S029    | 2025-01-15 14:00:00 | Selesai     | Membantu menyusun rencana studi semester depan.               | 5027211029    | 3578012345670009 | A004           | T019
 S030    | 2025-01-15 15:00:00 | Selesai     | Sesi relaksasi dan mindfulness.                               | 5028211030    | 3578012345670010 | A005           | T020
 S031    | 2025-02-16 10:00:00 | Selesai     | Mengatasi kecemasan sosial di kelas.                          | 5029211031    | 3578012345670002 | A001           | T007
 S032    | 2025-02-16 11:00:00 | Selesai     | Konsultasi portofolio desain.                                 | 5030211032    | 3578012345670001 | A002           | T005
 S033    | 2025-02-17 13:00:00 | Dijadwalkan |                                                               | 5025211033    | 3578012345670003 | A003           | T002
 S034    | 2025-02-17 14:00:00 | Selesai     | Membantu mahasiswa beradaptasi dengan teman baru.             | 5026211034    | 3578012345670004 | A004           | T011
 S035    | 2025-02-18 09:00:00 | Selesai     | Membangun kepercayaan diri untuk presentasi.                  | 5027211035    | 3578012345670005 | A005           | T009
 S036    | 2025-02-18 10:00:00 | Selesai     | Manajemen stres karena tugas menumpuk.                        | 5028211036    | 3578012345670006 | A001           | T001
 S037    | 2025-02-19 11:00:00 | Selesai     | Mediasi konflik keluarga.                                     | 5029211037    | 3578012345670007 | A002           | T012
 S038    | 2025-02-19 13:00:00 | Dibatalkan  | Mahasiswa sakit.                                              | 5030211038    | 3578012345670008 | A003           | T014
 S039    | 2025-02-20 14:00:00 | Selesai     | Diskusi rencana studi dan pemilihan mata kuliah.              | 5025211039    | 3578012345670009 | A004           | T019
 S040    | 2025-02-20 15:00:00 | Selesai     | Mengatasi cemas dan overthinking.                             | 5026211040    | 3578012345670010 | A005           | T007
 S041    | 2025-03-21 10:00:00 | Selesai     | Sesi lanjutan prokrastinasi, sudah ada perbaikan.             | 5025211001    | 3578012345670003 | A001           | T002
 S042    | 2025-03-21 11:00:00 | Selesai     | Review CV final.                                              | 5025211002    | 3578012345670001 | A002           | T005
 S043    | 2025-03-22 13:00:00 | Selesai     | Latihan mindfulness rutin.                                    | 5026211003    | 3578012345670002 | A003           | T020
 S044    | 2025-03-22 14:00:00 | Dijadwalkan |                                                               | 5027211004    | 3578012345670004 | A004           | T006
 S045    | 2025-03-23 09:00:00 | Selesai     | Mengatasi quarter life crisis.                                | 5025211005    | 3578012345670005 | A005           | T008
 S046    | 2025-03-23 10:00:00 | Selesai     | Sesi tentang stres ujian tengah semester.                     | 5028211006    | 3578012345670006 | A001           | T001
 S047    | 2025-03-24 11:00:00 | Selesai     | Diskusi masalah komunikasi dengan orang tua.                  | 5029211007    | 3578012345670007 | A002           | T012
 S048    | 2025-03-24 13:00:00 | Selesai     | Latihan wawancara HRD.                                        | 5025211009    | 3578012345670008 | A003           | T004
 S049    | 2025-03-25 14:00:00 | Selesai     | Mengatasi burnout dan mengembalikan motivasi.                 | 5026211010    | 3578012345670009 | A004           | T013
 S050    | 2025-03-25 15:00:00 | Selesai     | Membantu mahasiswa yang merasa kesepian di perantauan.        | 5027211011    | 3578012345670010 | A005           | T016
 S051    | 2025-04-26 10:00:00 | Selesai     | Detoks media sosial.                                          | 5028211012    | 3578012345670002 | A001           | T015
 S052    | 2025-04-26 11:00:00 | Selesai     | Mencari jalur karir yang sesuai passion.                      | 5029211013    | 3578012345670001 | A002           | T014
 S053    | 2025-04-27 13:00:00 | Selesai     | Sesi evaluasi setelah ujian.                                  | 5025211001    | 3578012345670003 | A003           | T003
 S054    | 2025-04-27 14:00:00 | Selesai     | Latihan presentasi untuk tugas akhir.                         | 5030211014    | 3578012345670004 | A004           | T017
 S055    | 2025-04-28 09:00:00 | Selesai     | Membicarakan rencana masa depan.                              | 5025211015    | 3578012345670005 | A005           | T008
 S056    | 2025-04-28 10:00:00 | Selesai     | Sesi relaksasi.                                               | 5026211016    | 3578012345670006 | A001           | T020
 S057    | 2025-04-29 11:00:00 | Dibatalkan  | Jadwal bentrok.                                               | 5027211017    | 3578012345670007 | A002           | T012
 S058    | 2025-04-29 13:00:00 | Selesai     | Finalisasi CV dan surat lamaran.                              | 5028211018    | 3578012345670008 | A003           | T005
 S059    | 2025-04-30 14:00:00 | Selesai     | Review rencana studi.                                         | 5029211019    | 3578012345670009 | A004           | T019
 S060    | 2025-04-30 15:00:00 | Selesai     | Sesi penutup, mahasiswa merasa jauh lebih baik.               | 5030211020    | 3578012345670010 | A005           | T016
 S061    | 2025-05-01 09:00:00 | Dijadwalkan |                                                               | 5025211039    | 3578012345670001 | A001           | T004
 S062    | 2025-05-01 10:00:00 | Dijadwalkan |                                                               | 5026211040    | 3578012345670002 | A002           | T007
 S063    | 2025-05-02 11:00:00 | Dijadwalkan |                                                               | 5027211029    | 3578012345670003 | A003           | T002
 S064    | 2025-05-02 13:00:00 | Dijadwalkan |                                                               | 5028211030    | 3578012345670004 | A004           | T006
 S065    | 2025-05-03 14:00:00 | Dijadwalkan |                                                               | 5029211031    | 3578012345670005 | A005           | T009
(65 rows)


fp_mbd_backend=# SELECT * FROM topik;
 topik_id |               topik_nama                | admin_admin_id
----------+-----------------------------------------+----------------
 T001     | Manajemen Stres Ujian Akhir             | A001
 T002     | Prokrastinasi Akademik                  | A002
 T003     | Strategi Belajar Efektif                | A003
 T004     | Persiapan Karir dan Wawancara Kerja     | A004
 T005     | Pembuatan CV dan Portofolio             | A005
 T006     | Konflik dengan Teman atau Pasangan      | A001
 T007     | Mengatasi Rasa Cemas dan Panik          | A002
 T008     | Quarter-Life Crisis                     | A003
 T009     | Meningkatkan Kepercayaan Diri           | A004
 T010     | Manajemen Keuangan Pribadi              | A005
 T011     | Adaptasi di Lingkungan Kampus           | A001
 T012     | Masalah Keluarga                        | A002
 T013     | Burnout Akademik                        | A003
 T014     | Menentukan Pilihan Karir                | A004
 T015     | Kecanduan Media Sosial                  | A005
 T016     | Mengatasi Kesepian                      | A001
 T017     | Public Speaking Anxiety                 | A002
 T018     | Membangun Kebiasaan Positif             | A003
 T019     | Pemilihan Mata Kuliah dan Rencana Studi | A004
 T020     | Teknik Relaksasi dan Mindfulness        | A005
(20 rows)


fp_mbd_backend=# SELECT * FROM mahasiswa LIMIT 10;
    nrp     |      nama       |        departemen        |    kontak    | user_user_id
------------+-----------------+--------------------------+--------------+--------------
 5025211001 | Adi Nugraha     | Teknik Informatika       | 085712340001 | U016
 5025211002 | Bella Safira    | Sistem Informasi         | 085712340002 | U017
 5026211003 | Chandra Wijaya  | Manajemen Bisnis         | 085712340003 | U018
 5027211004 | Diana Putri     | Akuntansi                | 085712340004 | U019
 5025211005 | Erwin Prasetya  | Teknik Informatika       | 085712340005 | U020
 5028211006 | Farah Nabila    | Ilmu Komunikasi          | 085712340006 | U021
 5029211007 | Ganjar Aditama  | Desain Komunikasi Visual | 085712340007 | U022
 5030211008 | Hana Malika     | Teknik Elektro           | 085712340008 | U023
 5025211009 | Ivan Gunawan    | Teknik Informatika       | 085712340009 | U024
 5026211010 | Jenny Anggraini | Sistem Informasi         | 085712340010 | U025
(10 rows)


fp_mbd_backend=# \conninfo
You are connected to database "fp_mbd_backend" as user "postgres" on host "localhost" (address "::1") at port "5432".
fp_mbd_backend=#
```


# 8.

```bash
Login user

email :


pw :


```