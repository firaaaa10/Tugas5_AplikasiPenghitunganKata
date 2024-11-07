# Aplikasi Penghitung Kata
Tugas 5 - Siti Safira 2210010336
# 1. Deskripsi Program
• Gunakan JTextArea dalam JScrollPane untuk input teks

• Setelah menekan tombol Hitung, hasil perhitungan berupa jumlah
kata dan karakter ditampilkan pada beberapa JLabel

# 2. Komponen GUI: 
JFrame, JPanel, JLabel, JTextArea, JScrollPane, JButton
- JPanel sebagai container utama.
- JTextArea untuk input teks dan letakkan dalam JScrollPane.
- JButton dengan label “Hitung Kata” untuk memicu perhitungan, "Cari" untuk memicu hasil pencarian kata, "Hapus" untuk menghapus input dan hasil, "Simpan File" digunakan untuk memicu penyimpanan, dan "Keluar" untuk keluar dari project.
- beberapa JLabel untuk menampilkan hasil jumlah kata, karakter, kalimat, paragraf, dan jumlah kemunculan kata.
- JTextField untuk input kata yang ingin dicari.

- JButton dengan label "Hapus"
```
private void btnHapusActionPerformed(java.awt.event.ActionEvent evt) {                                         
    btnHapus.addActionListener((ActionEvent e) -> {
        textAreaInputKata.setText("");  // Mengosongkan JTextArea
        // Mereset label hasil perhitungan
        jumlahkata.setText("0");
        jumlahkarakter.setText("0");
        jumlahkalimat.setText("0");
        jumlahparagraf.setText("0");
        jumlahkemunculankata.setText("0");
        TextFieldCari.setText(""); // Mengosongkan JTextField untuk pencarian kata
    });

    }
```
Event ActionListener pada tombol ini untuk mengosongkan teks di JTextArea dan mengatur ulang label hasil perhitungan.
Dengan penambahan tombol "Hapus" ini, Anda dapat mengosongkan JTextArea dan mereset semua label perhitungan kembali ke nol secara langsung.

# 3. Logika Program: 
Manipulasi string, Ekspresi reguler


# 4. Events:
• ActionListener untuk tombol Hitung
```
private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {                                          
    // Tambahkan ActionListener pada tombol "Hitung"
    btnHitung.addActionListener((ActionEvent e) -> {
        hitungText(); // Memanggil metode countText() ketika tombol ditekan
    });
    
    }                                         
```
Penjelasan Kode :
hitungText() berfungsi untuk menghitung jumlah kata, karakter, kalimat, dan paragraf dalam teks.
ActionListener pada tombol "Hitung" memicu fungsi hitungText() ketika tombol ditekan.

- DocumentListener pada JTextArea memungkinkan perhitungan real-time saat teks diubah. 
```
// Method to count words, characters, sentences, and paragraphs
    private void hitungText() {
        String text = textAreaInputKata.getText();

        // Hitung jumlah kata
        int wordCount = text.isEmpty() ? 0 : text.split("\\s+").length;

        // Hitung jumlah karakter
        int charCount = text.length();

        // Hitung jumlah kalimat menggunakan pemisah .!? untuk mengenali akhir kalimat
        int sentenceCount = text.isEmpty() ? 0 : text.split("[.!?]").length;

        // Hitung jumlah paragraf berdasarkan garis baru ganda sebagai pemisah
        int paragraphCount = text.isEmpty() ? 0 : text.split("\\n+").length;

        // Update JLabel dengan hasil perhitungan
        jumlahkata.setText("" + wordCount);
        jumlahkarakter.setText("" + charCount);
        jumlahkalimat.setText("" + sentenceCount);
        jumlahparagraf.setText("" + paragraphCount);
```
Penjelasan Kode :
Fungsi ini digunakan untuk menghitung jumlah kata, karakter, kalimat, dan paragraf:
- Jumlah Kata: Menggunakan split("\\s+") untuk hitung jumlah kata.
- Jumlah Karakter: Menggunakan text.length() untuk menghitung karakter total.
- Jumlah Kalimat: Menggunakan split("[.!?]") untuk memisahkan kalimat berdasarkan tanda baca. Perhitungan kalimat dilakukan dengan text.split("[.!?]"), yang membagi teks berdasarkan titik (.), tanda seru (!), atau tanda tanya (?). Setiap tanda ini dianggap sebagai akhir sebuah kalimat.
- Jumlah Paragraf: Menggunakan split("\\n+") untuk menghitung jumlah paragraf berdasarkan garis baru ganda sebagai pemisah. Perhitungan paragraf dilakukan dengan text.split("\\n+"), yang memisahkan teks setiap kali ada baris baru (\n). Setiap baris baru dianggap sebagai awal paragraf baru, dan jeda baris ganda (\n\n) dianggap sebagai pemisah antar paragraf.

• DocumentListener pada JTextArea untuk menghitung secara realtime
```
// Add DocumentListener to JTextArea for real-time counting
        textAreaInputKata.getDocument().addDocumentListener(new DocumentListener() {
            public void changedUpdate(DocumentEvent e) { hitungText(); }
            public void removeUpdate(DocumentEvent e) { hitungText(); }
            public void insertUpdate(DocumentEvent e) { hitungText(); }
        });    
    }
```
Kode DocumentListener ini akan memanggil metode hitungText() setiap kali ada perubahan di textArea, baik saat teks ditambahkan atau dihapus, sehingga memungkinkan aplikasi untuk menghitung jumlah kata, karakter, kalimat, dan paragraf secara real-time.

# 5. Variasi:
• Tambahkan fitur untuk menghitung jumlah kalimat dan paragraf
```
 // Hitung jumlah kalimat menggunakan pemisah .!? untuk mengenali akhir kalimat
    int sentenceCount = text.isEmpty() ? 0 : text.split("[.!?]").length;

 // Hitung jumlah paragraf berdasarkan garis baru ganda sebagai pemisah
    int paragraphCount = text.isEmpty() ? 0 : text.split("\\n+").length;

// Update JLabel dengan hasil perhitungan
    jumlahkalimat.setText("" + sentenceCount);
    jumlahparagraf.setText("" + paragraphCount);
```
• Implementasikan fungsi pencarian kata tertentu dalam teks
```
 private void btnCariActionPerformed(java.awt.event.ActionEvent evt) {                                        
    // Add ActionListener to search button
        btnCari.addActionListener((ActionEvent e) -> {
            CariKata();
        });
    }   
```
Penjelasan :
Metode CariKata() menghitung jumlah kemunculan kata yang sesuai di dalam teks dan memperbarui jumlahkemunculankata.
```
 // Method to search a specific word
    private void CariKata() {
        String text = textAreaInputKata.getText();
        String searchWord = TextFieldCari.getText();
        int count = 0;

        if (!searchWord.isEmpty()) {
            String[] words = text.split("\\s+");
            for (String word : words) {
                if (word.equalsIgnoreCase(searchWord)) {
                    count++;
                }
            }
        }
        
        jumlahkemunculankata.setText(" " + count);
    }
```
  
• Sediakan opsi untuk menyimpan teks dan hasil perhitungan ke file
```
private void btnSimpanActionPerformed(java.awt.event.ActionEvent evt) {                                          
    // Add ActionListener to save button
        btnSimpan.addActionListener((ActionEvent e) -> {
            SimpanFile();
        });
    }      
```
Metode SimpanFile() membuat file hasil_penghitungan.txt dan menulis teks yang diinput beserta hasil perhitungan.
Jika penyimpanan berhasil, pesan konfirmasi akan ditampilkan.
```
// Method to save the text and results to a file
    private void SimpanFile() {
    JFileChooser fileChooser = new JFileChooser();
    fileChooser.setDialogTitle("Simpan Hasil Penghitungan");
    int userSelection = fileChooser.showSaveDialog(this);
    
    if (userSelection == JFileChooser.APPROVE_OPTION) {
        try (FileWriter writer = new FileWriter(fileChooser.getSelectedFile())) {
       
            writer.write("Teks:\n" + textAreaInputKata.getText() + "\n\n");
            writer.write("Jumlah Kata: " + jumlahkata.getText() + "\n");
            writer.write("Jumlah Karakter: " + jumlahkarakter.getText() + "\n");
            writer.write("Jumlah Kalimat: " + jumlahkalimat.getText() + "\n");
            writer.write("Jumlah Paragraf: " + jumlahparagraf.getText() + "\n");
            writer.write("Pencarian Kata '" + TextFieldCari.getText() + "': " + jumlahkemunculankata.getText() + "\n");
            JOptionPane.showMessageDialog(this, "Hasil berhasil disimpan ke hasil_penghitungan.txt");
        } catch (IOException e) {
            JOptionPane.showMessageDialog(this, "Gagal menyimpan file: " + e.getMessage());
        }
        }
    }
```
Dengan kode ini, sebuah dialog JFileChooser akan muncul sehingga Anda bisa memilih atau menentukan lokasi penyimpanan file hasil penghitungan sesuai keinginan.


## Contoh Gambar Project Setelah di Run
![](https://github.com/firaaaa10/Tugas5_AplikasiPenghitunganKata/blob/main/Cuplikan%20layar%202024-11-07%20194302.png)

## Indikator Penilaian:

| No  | Komponen         |  Persentase  |
| :-: | --------------   |   :-----:    |
|  1  | Komponen GUI     |    20    |
|  2  | Logika Program   |    20    |
|  3  | Kesesuaian UI    |    15    |
|  4  | Constructor      |    15    |
|  5  | Memenuhi Variasi |    30    |
|     | *TOTAL*        | *100* |

## Pembuat

Nama  : Siti Safira
NPM   : 2210010336
