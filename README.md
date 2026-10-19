# gRPC Polyglot Lab

Praktikum komunikasi inter-service dengan gRPC: satu server Go dilayani oleh client Python dan Node.js melalui satu kontrak user.proto.

## Analisis Pendekatan Kompilasi

Pada Go dan Python digunakan pendekatan static code generation. File user.proto dikompilasi terlebih dahulu oleh protoc (beserta plugin-nya) menjadi kode sumber nyata, seperti user.pb.go dan user_pb2.py, yang kemudian menjadi bagian dari proyek. Keuntungannya adalah type safety, dukungan autocompletion di IDE, dan kesalahan yang terdeteksi lebih awal. Kekurangannya, setiap kali skema berubah, kode harus di-generate ulang secara manual. Pada Node.js digunakan pendekatan dynamic runtime generation: pustaka @grpc/proto-loader membaca dan mem-parsing user.proto saat program dijalankan, lalu membentuk objek service secara dinamis tanpa langkah kompilasi dan tanpa file hasil generate. Pendekatan ini lebih praktis dan fleksibel karena perubahan skema langsung terbaca saat program dijalankan ulang, tetapi tidak memiliki pengecekan tipe saat kompilasi dan ada sedikit overhead parsing saat startup.
