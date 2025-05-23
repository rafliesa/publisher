## How much data your publisher program will send to the message broker in one run?
Program publisher ini dirancang untuk mengirimkan lima (5) pesan dalam satu kali eksekusi. Hal ini terlihat dari lima kali pemanggilan fungsi publish_event, di mana setiap pemanggilan mengirimkan satu pesan bertipe UserCreatedEventMessage. Masing-masing pesan memuat dua field, yaitu user_id yang berupa string angka dari "1" hingga "5", dan user_name yang merupakan string berisi NPM "2306202694" diikuti dengan nama yang berbeda: "Amir", "Budi", "Cica", "Dira", dan "Emir". Semua pesan tersebut dikirim ke antrian bernama "user_created" yang dikelola oleh broker pesan berbasis AMQP. Secara teknis, ukuran setiap pesan dipengaruhi oleh hasil serialisasi struktur UserCreatedEventMessage menggunakan Borsh, namun dari sisi fungsional, program ini secara eksplisit mengirimkan lima buah pesan ke broker.

## The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?
Penggunaan URL yang sama, yaitu "amqp://guest:guest@localhost:5672", dalam program publisher dan subscriber menunjukkan bahwa keduanya terhubung ke broker pesan AMQP yang sama. Kesamaan ini memastikan bahwa kedua program beroperasi pada server broker yang identik—berlokasi di mesin lokal (localhost) dan menggunakan port standar AMQP (5672), serta melakukan autentikasi dengan kredensial yang sama (username dan password: guest). Dengan konfigurasi ini, publisher dapat mengirimkan pesan ke antrian bernama "user_created", sementara subscriber dapat menerima pesan dari antrian yang sama. Kedua program tidak perlu saling mengenal atau terhubung secara langsung, melainkan cukup mengetahui cara mengakses broker pesan sebagai perantara komunikasi. Pola ini menciptakan sistem yang asinkron, terpisah secara longgar (loosely coupled), dan tangguh, karena komponen-komponennya dapat berjalan secara independen dan tetap berfungsi meskipun tidak dijalankan secara bersamaan.

##
![image](https://github.com/user-attachments/assets/40ccc180-7f29-4434-ba7f-16af5ebba5f6)

##
![image](https://github.com/user-attachments/assets/4d99392c-342c-4168-8afb-82c2cffbbe4b)
![image](https://github.com/user-attachments/assets/410d7021-e49d-435d-a7c7-7460a8c56a81)
