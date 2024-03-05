
**jam digital**

import javax.swing.*;
import java.awt.*;
import java.text.SimpleDateFormat;
import java.util.Calendar;

public class jamdigital extends JFrame {

    Calendar calendar;
    SimpleDateFormat timeFormat;
    SimpleDateFormat dayFormat;
    SimpleDateFormat dateFormat;

    JLabel timeLabel;
    JLabel dayLabel;
    JLabel dateLabel;
    String time;
    String day;
    String date;
    jamdigital() {
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        this.setTitle("Jam Digital");
        this.setLayout(new FlowLayout());
        this.setSize(350, 220);
        this.setResizable(false);

        timeFormat = new SimpleDateFormat("hh:mm:ss a");
        dayFormat=new SimpleDateFormat("EEEE");
        dateFormat=new SimpleDateFormat("dd MMMMM, yyyy");
        timeLabel = new JLabel();
        timeLabel.setFont(new Font("Times_New_Roman", Font.PLAIN, 59));
        timeLabel.setBackground(Color.RED);
        timeLabel.setForeground(Color.white);
        timeLabel.setOpaque(true);
        dayLabel=new JLabel();
        dayLabel.setFont(new Font("Times_New_Roman",Font.BOLD,34));

        dateLabel=new JLabel();
        dateLabel.setFont(new Font("Times_New_Roman",Font.BOLD,30));


        this.add(timeLabel);
        this.add(dayLabel);
        this.add(dateLabel);
        this.setVisible(true);

        setTimer();
    }

    public void setTimer() {
        while (true) {
            time = timeFormat.format(Calendar.getInstance().getTime());
            timeLabel.setText(time);

            day = dayFormat.format(Calendar.getInstance().getTime());
            dayLabel.setText(day);

            date = dateFormat.format(Calendar.getInstance().getTime());
            dateLabel.setText(date);

            try {
                Thread.sleep(1000);
            } catch (Exception e) {
                e.getStackTrace();
            }
        }
    }
    public static void main(String[] args) {
        new jamdigital();
    }
} 


**bayaran bil listrik**

import java.util.Scanner;

class Pelanggan {
    private String nama;
    private int idPelanggan;
    private MeteranListrik meteran;

    public Pelanggan(String nama, int idPelanggan) {
        this.nama = nama;
        this.idPelanggan = idPelanggan;
        this.meteran = new MeteranListrik();
    }

    public String getNama() {
        return nama;
    }

    public int getIdPelanggan() {
        return idPelanggan;
    }

    public MeteranListrik getMeteran() {
        return meteran;
    }
}

class MeteranListrik {
    private double pembacaanSaatIni;
    private double pembacaanSebelumnya;
    private double tarifPerUnit = 0.10; // tarif per unit dalam dollar

    public void setPembacaanSaatIni(double pembacaanSaatIni) {
        this.pembacaanSaatIni = pembacaanSaatIni;
    }

    public void setPembacaanSebelumnya(double pembacaanSebelumnya) {
        this.pembacaanSebelumnya = pembacaanSebelumnya;
    }

    public double hitungTagihan() {
        return (pembacaanSaatIni - pembacaanSebelumnya) * tarifPerUnit;
    }
}

public class SistemTagihanListrik {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Masukkan nama pelanggan: ");
        String nama = scanner.nextLine();
        System.out.print("Masukkan ID pelanggan: ");
        int idPelanggan = scanner.nextInt();

        Pelanggan pelanggan = new Pelanggan(nama, idPelanggan);

        System.out.print("Masukkan pembacaan meteran sebelumnya: ");
        double pembacaanSebelumnya = scanner.nextDouble();
        pelanggan.getMeteran().setPembacaanSebelumnya(pembacaanSebelumnya);

        System.out.print("Masukkan pembacaan meteran saat ini: ");
        double pembacaanSaatIni = scanner.nextDouble();
        pelanggan.getMeteran().setPembacaanSaatIni(pembacaanSaatIni);

        double jumlahTagihan = pelanggan.getMeteran().hitungTagihan();

        System.out.println("Pelanggan: " + pelanggan.getNama());
        System.out.println("ID Pelanggan: " + pelanggan.getIdPelanggan());
        System.out.println("Jumlah Tagihan: $" + jumlahTagihan);

        scanner.close();
    }
}
