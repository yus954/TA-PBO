import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

class ParkingSystem {
    private static Map<String, ParkingRecord> parkingRecords = new HashMap<>();
    private static int parkingRatePerHour = 10;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("=== Sistem Lahan Parkir ===");
            System.out.println("1. Login Admin Parkir");
            System.out.println("2. Check-in Kendaraan");
            System.out.println("3. Check-out Kendaraan");
            System.out.println("4. Lihat Daftar Mobil Sedang Parkir");
            System.out.println("5. Lihat Semua Daftar Mobil yang Pernah Parkir");
            System.out.println("6. Keluar");
            System.out.print("Pilihan Anda: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    loginAdmin();
                    break;
                case 2:
                    checkIn();
                    break;
                case 3:
                    checkOut();
                    break;
                case 4:
                    viewCurrentlyParkedCars();
                    break;
                case 5:
                    viewAllParkingRecords();
                    break;
                case 6:
                    System.out.println("Terima kasih!");
                    break;
                default:
                    System.out.println("Pilihan tidak valid. Silakan coba lagi.");
            }
        } while (choice != 6);
    }

    private static void loginAdmin() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Masukkan username admin: ");
        String username = scanner.nextLine();
        System.out.print("Masukkan password admin: ");
        String password = scanner.nextLine();

        // Proses otentikasi admin (implementasi sederhana)
        if (isValidAdmin(username, password)) {
            System.out.println("Login admin berhasil!");
        } else {
            System.out.println("Login admin gagal. Username atau password salah.");
        }
    }

    private static boolean isValidAdmin(String username, String password) {
        // Simulasi data admin yang sah
        String validUsername = "admin";
        String validPassword = "admin123";

        // Proses verifikasi
        return username.equals(validUsername) && password.equals(validPassword);
    }


    private static void checkIn() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Masukkan plat nomor kendaraan: ");
        String plateNumber = scanner.nextLine();
        System.out.print("Masukkan tanggal dan jam masuk (format: yyyy-MM-dd HH:mm): ");
        String entryTime = scanner.nextLine();

        ParkingRecord record = new ParkingRecord(plateNumber, entryTime);
        parkingRecords.put(plateNumber, record);

        System.out.println("Kendaraan berhasil check-in.");
    }

    private static void checkOut() {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Masukkan plat nomor kendaraan: ");
        String plateNumber = scanner.nextLine();

        if (parkingRecords.containsKey(plateNumber)) {
            ParkingRecord record = parkingRecords.get(plateNumber);
            record.setExitTime(); // Set waktu keluar ke waktu saat ini

            // Hitung biaya parkir
            int hoursParked = record.calculateParkingDuration();
            int parkingFee = hoursParked * parkingRatePerHour;

            // Cetak detail struk
            System.out.println("=== Struk Parkir ===");
            System.out.println("Plat Nomor: " + record.getPlateNumber());
            System.out.println("Jam Masuk: " + record.getEntryTime());
            System.out.println("Jam Keluar: " + record.getExitTime());
            System.out.println("Durasi Parkir: " + hoursParked + " jam");
            System.out.println("Biaya Parkir: Rp" + parkingFee);
        } else {
            System.out.println("Kendaraan tidak ditemukan.");
        }
    }

    private static void viewCurrentlyParkedCars() {
        System.out.println("=== Daftar Mobil Sedang Parkir ===");
        for (ParkingRecord record : parkingRecords.values()) {
            if (record.getExitTime() == null) {
                System.out.println("Plat Nomor: " + record.getPlateNumber());
                System.out.println("Jam Masuk: " + record.getEntryTime());
                System.out.println();
            }
        }
    }

    private static void viewAllParkingRecords() {
        System.out.println("=== Semua Daftar Mobil yang Pernah Parkir ===");
        for (ParkingRecord record : parkingRecords.values()) {
            System.out.println("Plat Nomor: " + record.getPlateNumber());
            System.out.println("Jam Masuk: " + record.getEntryTime());
            System.out.println("Jam Keluar: " + record.getExitTime());
            System.out.println();
        }
    }
}

class ParkingRecord {
    private String plateNumber;
    private String entryTime;
    private String exitTime;

    public ParkingRecord(String plateNumber, String entryTime) {
        this.plateNumber = plateNumber;
        this.entryTime = entryTime;
    }

    public String getPlateNumber() {
        return plateNumber;
    }

    public String getEntryTime() {
        return entryTime;
    }

    public String getExitTime() {
        return exitTime;
    }

    public void setExitTime() {
        this.exitTime = getCurrentTime();
    }

    public int calculateParkingDuration() {
        return 0;
    }

    private String getCurrentTime() {
        return "";
    }
}
