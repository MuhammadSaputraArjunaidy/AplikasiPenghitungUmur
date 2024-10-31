
# Project Title

    Aplikasi Penghitungan Umur

# Deskripsi
    Aplikasi ini menggunakan komponen JFrame untuk membangun antarmuka pengguna yang interaktif. Pengguna dapat memasukkan tanggal lahir mereka melalui dateChooser, dan aplikasi akan menampilkan usia dalam tahun, bulan, dan hari. Selain itu, aplikasi ini mengambil data dari API untuk menampilkan peristiwa sejarah yang terjadi pada tanggal ulang tahun pengguna.
# Code Penghitungan Umur

## Penghitung Umur Frame
```java
        import java.time.LocalDate;
        import java.time.ZoneId;
        import java.time.format.DateTimeFormatter;
        import java.util.Date;

        public class PenghitungUmurFrame extends javax.swing.JFrame {

            private PenghitungUmurHelper helper;
            private volatile boolean stopFetching = false;
            private Thread peristiwaThread;

        
            public PenghitungUmurFrame() {
                initComponents();
                helper = new PenghitungUmurHelper();
            }

        
            @SuppressWarnings("unchecked")
            // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
            private void initComponents() {

                jPanel1 = new javax.swing.JPanel();
                jLabel1 = new javax.swing.JLabel();
                jPanel2 = new javax.swing.JPanel();
                btnHitung = new javax.swing.JButton();
                txtUmur = new javax.swing.JTextField();
                txtHariUlangTahunBerikutnya = new javax.swing.JTextField();
                jLabel2 = new javax.swing.JLabel();
                jLabel3 = new javax.swing.JLabel();
                jLabel4 = new javax.swing.JLabel();
                btnKeluar = new javax.swing.JButton();
                dateChooserTanggalLahir = new com.toedter.calendar.JDateChooser();
                jPanel3 = new javax.swing.JPanel();
                jScrollPane1 = new javax.swing.JScrollPane();
                txtAreaPeristiwa = new javax.swing.JTextArea();

                setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

                jLabel1.setBackground(new java.awt.Color(153, 204, 255));
                jLabel1.setFont(new java.awt.Font("Times New Roman", 1, 24)); // NOI18N
                jLabel1.setText("Aplikasi Penghitung Umur");

                javax.swing.GroupLayout jPanel1Layout = new javax.swing.GroupLayout(jPanel1);
                jPanel1.setLayout(jPanel1Layout);
                jPanel1Layout.setHorizontalGroup(
                    jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel1Layout.createSequentialGroup()
                        .addGap(186, 186, 186)
                        .addComponent(jLabel1)
                        .addContainerGap(javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
                );
                jPanel1Layout.setVerticalGroup(
                    jPanel1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel1Layout.createSequentialGroup()
                        .addGap(26, 26, 26)
                        .addComponent(jLabel1)
                        .addContainerGap(27, Short.MAX_VALUE))
                );

                jPanel2.addPropertyChangeListener(new java.beans.PropertyChangeListener() {
                    public void propertyChange(java.beans.PropertyChangeEvent evt) {
                        jPanel2PropertyChange(evt);
                    }
                });

                btnHitung.setText("Hitung");
                btnHitung.addActionListener(new java.awt.event.ActionListener() {
                    public void actionPerformed(java.awt.event.ActionEvent evt) {
                        btnHitungActionPerformed(evt);
                    }
                });

                jLabel2.setText("Pilih Tanggal Lahir");

                jLabel3.setText("Umur Anda");

                jLabel4.setText("Hari ulang Tahun Berikutnya");

                btnKeluar.setText("Keluar");
                btnKeluar.addActionListener(new java.awt.event.ActionListener() {
                    public void actionPerformed(java.awt.event.ActionEvent evt) {
                        btnKeluarActionPerformed(evt);
                    }
                });

                dateChooserTanggalLahir.setDateFormatString("dd-MM-yyyy");
                dateChooserTanggalLahir.addPropertyChangeListener(new java.beans.PropertyChangeListener() {
                    public void propertyChange(java.beans.PropertyChangeEvent evt) {
                        dateChooserTanggalLahirPropertyChange(evt);
                    }
                });

                javax.swing.GroupLayout jPanel2Layout = new javax.swing.GroupLayout(jPanel2);
                jPanel2.setLayout(jPanel2Layout);
                jPanel2Layout.setHorizontalGroup(
                    jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addGap(26, 26, 26)
                        .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addGroup(jPanel2Layout.createSequentialGroup()
                                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                                    .addComponent(jLabel2)
                                    .addComponent(jLabel3))
                                .addGap(68, 68, 68)
                                .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                                    .addGroup(jPanel2Layout.createSequentialGroup()
                                        .addComponent(dateChooserTanggalLahir, javax.swing.GroupLayout.DEFAULT_SIZE, 226, Short.MAX_VALUE)
                                        .addGap(44, 44, 44)
                                        .addComponent(btnHitung, javax.swing.GroupLayout.PREFERRED_SIZE, 86, javax.swing.GroupLayout.PREFERRED_SIZE)
                                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                                        .addComponent(btnKeluar))
                                    .addGroup(jPanel2Layout.createSequentialGroup()
                                        .addComponent(txtUmur, javax.swing.GroupLayout.PREFERRED_SIZE, 233, javax.swing.GroupLayout.PREFERRED_SIZE)
                                        .addGap(0, 0, Short.MAX_VALUE))))
                            .addGroup(jPanel2Layout.createSequentialGroup()
                                .addComponent(jLabel4)
                                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.UNRELATED)
                                .addComponent(txtHariUlangTahunBerikutnya, javax.swing.GroupLayout.PREFERRED_SIZE, 233, javax.swing.GroupLayout.PREFERRED_SIZE)
                                .addGap(0, 0, Short.MAX_VALUE)))
                        .addContainerGap())
                );
                jPanel2Layout.setVerticalGroup(
                    jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(jPanel2Layout.createSequentialGroup()
                        .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addComponent(jLabel2)
                            .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                                .addComponent(btnHitung)
                                .addComponent(btnKeluar))
                            .addComponent(dateChooserTanggalLahir, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                        .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                            .addGroup(jPanel2Layout.createSequentialGroup()
                                .addGap(19, 19, 19)
                                .addComponent(jLabel3))
                            .addGroup(jPanel2Layout.createSequentialGroup()
                                .addGap(18, 18, 18)
                                .addComponent(txtUmur, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)))
                        .addGap(21, 21, 21)
                        .addGroup(jPanel2Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                            .addComponent(jLabel4)
                            .addComponent(txtHariUlangTahunBerikutnya, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                        .addContainerGap(javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
                );

                javax.swing.GroupLayout jPanel3Layout = new javax.swing.GroupLayout(jPanel3);
                jPanel3.setLayout(jPanel3Layout);
                jPanel3Layout.setHorizontalGroup(
                    jPanel3Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGap(0, 0, Short.MAX_VALUE)
                );
                jPanel3Layout.setVerticalGroup(
                    jPanel3Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGap(0, 0, Short.MAX_VALUE)
                );

                txtAreaPeristiwa.setColumns(20);
                txtAreaPeristiwa.setRows(5);
                jScrollPane1.setViewportView(txtAreaPeristiwa);

                javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
                getContentPane().setLayout(layout);
                layout.setHorizontalGroup(
                    layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                        .addContainerGap()
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                            .addComponent(jPanel1, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                            .addGroup(layout.createSequentialGroup()
                                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                                    .addComponent(jScrollPane1)
                                    .addComponent(jPanel2, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE))
                                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                                .addComponent(jPanel3, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)))
                        .addContainerGap())
                );
                layout.setVerticalGroup(
                    layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(layout.createSequentialGroup()
                        .addContainerGap()
                        .addComponent(jPanel1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                        .addComponent(jPanel2, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                        .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING, false)
                            .addComponent(jPanel3, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                            .addComponent(jScrollPane1, javax.swing.GroupLayout.DEFAULT_SIZE, 323, Short.MAX_VALUE))
                        .addContainerGap(31, Short.MAX_VALUE))
                );

                pack();
            }// </editor-fold>                        

            private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {                                          
                Date tanggalLahir = dateChooserTanggalLahir.getDate();
                if (tanggalLahir != null) {
                    // Menghitung umur dan hari ulang tahun berikutnya
                    LocalDate lahir
                            = tanggalLahir.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();
                    LocalDate sekarang = LocalDate.now();
                    String umur = helper.hitungUmurDetail(lahir, sekarang);
                    txtUmur.setText(umur);

                    // Menghitung tanggal ulang tahun berikutnya
                    LocalDate ulangTahunBerikutnya
                            = helper.hariUlangTahunBerikutnya(lahir, sekarang);
                    String hariUlangTahunBerikutnya
                            = helper.getDayOfWeekInIndonesian(ulangTahunBerikutnya);
                    DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");

                    String tanggalUlangTahunBerikutnya = ulangTahunBerikutnya.format(formatter);
                    txtHariUlangTahunBerikutnya.setText(hariUlangTahunBerikutnya + "(" + tanggalUlangTahunBerikutnya + ")");
                    
                    stopFetching = true;
                if (peristiwaThread != null && peristiwaThread.isAlive()) {
                    peristiwaThread.interrupt(); // Beri sinyal ke thread untuk berhenti
                }
        // Reset flag untuk thread baru
                stopFetching = false;
        // Mendapatkan peristiwa penting secara asinkron
                peristiwaThread = new Thread(() -> {
                    try {
                        txtAreaPeristiwa.setText("Tunggu, sedang mengambil data...\n");
                        helper.getPeristiwaBarisPerBaris(ulangTahunBerikutnya,txtAreaPeristiwa, () -> stopFetching);
                        if (!stopFetching) {
                            javax.swing.SwingUtilities.invokeLater(()
                                    -> txtAreaPeristiwa.append("Selesai mengambil data peristiwa"));
                        }
                    } catch (Exception e) {
                        if (Thread.currentThread().isInterrupted()) {
                            javax.swing.SwingUtilities.invokeLater(()
                                    -> txtAreaPeristiwa.setText("Pengambilan data dibatalkan.\n"));
                        }

                    }
                });
                peristiwaThread.start();
                }
                // Set stop flag untuk thread sebelumnya
                
            }                                         

            private void btnKeluarActionPerformed(java.awt.event.ActionEvent evt) {                                          
                System.exit(0);
            }                                         

            private void dateChooserTanggalLahirPropertyChange(java.beans.PropertyChangeEvent evt) {                                                       
                txtUmur.setText("");
                txtHariUlangTahunBerikutnya.setText("");        // TODO add your handling code here:
            }                                                      

            private void jPanel2PropertyChange(java.beans.PropertyChangeEvent evt) {                                       
                // Hentikan thread yang sedang berjalan saat tanggal lahir berubah
                stopFetching = true;
                if (peristiwaThread != null && peristiwaThread.isAlive()) {
                    peristiwaThread.interrupt();
                }
                txtAreaPeristiwa.setText("");
            }                                      

            /**
            * @param args the command line arguments
            */
            public static void main(String args[]) {
                /* Set the Nimbus look and feel */
                //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
                /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
                * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
                */
                try {
                    for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                        if ("Nimbus".equals(info.getName())) {
                            javax.swing.UIManager.setLookAndFeel(info.getClassName());
                            break;
                        }
                    }
                } catch (ClassNotFoundException ex) {
                    java.util.logging.Logger.getLogger(PenghitungUmurFrame.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
                } catch (InstantiationException ex) {
                    java.util.logging.Logger.getLogger(PenghitungUmurFrame.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
                } catch (IllegalAccessException ex) {
                    java.util.logging.Logger.getLogger(PenghitungUmurFrame.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
                } catch (javax.swing.UnsupportedLookAndFeelException ex) {
                    java.util.logging.Logger.getLogger(PenghitungUmurFrame.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
                }
                //</editor-fold>

                /* Create and display the form */
                java.awt.EventQueue.invokeLater(new Runnable() {
                    public void run() {
                        new PenghitungUmurFrame().setVisible(true);
                    }
                });
            }

            // Variables declaration - do not modify                     
            private javax.swing.JButton btnHitung;
            private javax.swing.JButton btnKeluar;
            private com.toedter.calendar.JDateChooser dateChooserTanggalLahir;
            private javax.swing.JLabel jLabel1;
            private javax.swing.JLabel jLabel2;
            private javax.swing.JLabel jLabel3;
            private javax.swing.JLabel jLabel4;
            private javax.swing.JPanel jPanel1;
            private javax.swing.JPanel jPanel2;
            private javax.swing.JPanel jPanel3;
            private javax.swing.JScrollPane jScrollPane1;
            private javax.swing.JTextArea txtAreaPeristiwa;
            private javax.swing.JTextField txtHariUlangTahunBerikutnya;
            private javax.swing.JTextField txtUmur;
            // End of variables declaration                   

        }
```

## Penghitungan Umur helper
```java
    
import java.time.LocalDate;
import java.time.Period;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.function.Supplier;
import javax.swing.JTextArea;
import org.json.JSONArray;
import org.json.JSONObject;

public class PenghitungUmurHelper {

    // Menerjemahkan teks ke bahasa Indonesia
    private String translateToIndonesian(String text) {
        try {
            String urlString = "https://lingva.ml/api/v1/en/id/"
                    + text.replace(" ", "%20");
            URL url = new URL(urlString);
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET");
            conn.setRequestProperty("User-Agent", "Mozilla/5.0");
            int responseCode = conn.getResponseCode();
            if (responseCode != 200) {
                throw new Exception("HTTP response code: " + responseCode);
            }
            BufferedReader in = new BufferedReader(new InputStreamReader(conn.getInputStream(), "utf-8"));
            String inputLine;
            StringBuilder content = new StringBuilder();
            while ((inputLine = in.readLine()) != null) {
                content.append(inputLine);
            }
            in.close();
            conn.disconnect();
            JSONObject json = new JSONObject(content.toString());
            return json.getString("translation");
        } catch (Exception e) {
            return text + " (Gagal diterjemahkan)";
        }
    }
    // Menghitung umur secara detail (tahun, bulan, hari)

    public String hitungUmurDetail(LocalDate lahir, LocalDate sekarang) {
        Period period = Period.between(lahir, sekarang);
        return period.getYears() + " tahun, " + period.getMonths() + "bulan, " + period.getDays() + " hari";
    }

    // Mendapatkan peristiwa penting secara baris per baris
    public void getPeristiwaBarisPerBaris(LocalDate tanggal, JTextArea txtAreaPeristiwa, Supplier<Boolean> shouldStop) {
        try {
            // Periksa jika thread seharusnya dihentikan sebelum dimulai
            if (shouldStop.get()) {
                return;
            }
            String urlString = "https://byabbe.se/on-this-day/"
                    + tanggal.getMonthValue() + "/" + tanggal.getDayOfMonth() + "/events.json";
            URL url = new URL(urlString);
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET");
            conn.setRequestProperty("User-Agent", "Mozilla/5.0");
            int responseCode = conn.getResponseCode();
            if (responseCode != 200) {
                throw new Exception("HTTP response code: " + responseCode + ". Silakan coba lagi nanti atau cek koneksi internet.");
            }
            BufferedReader in = new BufferedReader(new InputStreamReader(conn.getInputStream()));
            String inputLine;
            StringBuilder content = new StringBuilder();
            while ((inputLine = in.readLine()) != null) {
                // Periksa jika thread seharusnya dihentikan saat membacadata
                if (shouldStop.get()) {
                    in.close();
                    conn.disconnect();
                    javax.swing.SwingUtilities.invokeLater(()
                            -> txtAreaPeristiwa.setText("Pengambilan data dibatalkan.\n"));
                    return;
                }
                content.append(inputLine);
            }
            in.close();
            conn.disconnect();
            JSONObject json = new JSONObject(content.toString());
            JSONArray events = json.getJSONArray("events");
            for (int i = 0; i < events.length(); i++) {
                // Periksa jika thread seharusnya dihentikan sebelummemproses data
                if (shouldStop.get()) {
                    javax.swing.SwingUtilities.invokeLater(()
                            -> txtAreaPeristiwa.setText("Pengambilan data dibatalkan.\n"));
                    return;
                }
                JSONObject event = events.getJSONObject(i);
                String year = event.getString("year");
                String description = event.getString("description");
                String translatedDescription = translateToIndonesian(description);
                String peristiwa = year + ": " + translatedDescription;

                javax.swing.SwingUtilities.invokeLater(()
                        -> txtAreaPeristiwa.append(peristiwa + "\n"));
            }
            if (events.length() == 0) {
                javax.swing.SwingUtilities.invokeLater(()
                        -> txtAreaPeristiwa.setText(
                                "Tidak ada peristiwa penting yang ditemukan padatanggal ini."));
            }
        } catch (Exception e) {
            javax.swing.SwingUtilities.invokeLater(()
                    -> txtAreaPeristiwa.setText("Gagal mendapatkan data peristiwa: "
                            + e.getMessage()));
        }
    }

    // Menghitung hari ulang tahun berikutnya
    public LocalDate hariUlangTahunBerikutnya(LocalDate lahir, LocalDate sekarang) {
        LocalDate ulangTahunBerikutnya
                = lahir.withYear(sekarang.getYear());
        if (!ulangTahunBerikutnya.isAfter(sekarang)) {
            ulangTahunBerikutnya = ulangTahunBerikutnya.plusYears(1);
        }
        return ulangTahunBerikutnya;
    }

    // Menerjemahkan teks hari ke bahasa Indonesia
    public String getDayOfWeekInIndonesian(LocalDate date) {
        switch (date.getDayOfWeek()) {
            case MONDAY:
                return "Senin";
            case TUESDAY:
                return "Selasa";
            case WEDNESDAY:
                return "Rabu";
            case THURSDAY:
                return "Kamis";
            case FRIDAY:
                return "Jumat";
            case SATURDAY:
                return "Sabtu";
            case SUNDAY:
                return "Minggu";
            default:
                return "";
        }
    }
}

```

## Authors

    Muhammad Saputra Arjunaidy 
    2210010300
    5B Reg Pagi Banjarmasin

    https://github.com/MuhammadSaputraArjunaidy


## Features

    Fitur utama aplikasi ini meliputi:
    Penghitungan Usia: Menghitung dan menampilkan usia dalam format tahun, bulan, dan hari.
    Tanggal Ulang Tahun Berikutnya: Menampilkan tanggal ulang tahun berikutnya serta hari dalam seminggu.
    Peristiwa Sejarah: Mengambil dan menampilkan peristiwa-peristiwa penting yang terjadi pada tanggal yang sama di masa lalu.


## Screenshot
![Screenshot 2024-10-31 153000](https://github.com/user-attachments/assets/6d7f07c9-df31-4675-8a92-af2c78e193c9)

    
