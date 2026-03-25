# OOP-Project-Decision-Maker with Cost Benefit Analysis
Program berbasis Java ini dibuat berdasarkan *problem* yang terjadi ketika bingung mengambil sebuah keputusan di kehidupannya. Metode ini membantu *user* bisa mempertimbangkan keputusannya secara rasional dengan metode **Cost Benefit Analysis**

## Deskripsi Kasus
Dalam kehidupan sehari-hari, kita sering dihadapkan pada pilihan yang sulit, misalnya memilih antara tetap di kampus saat ini atau pindah kampus, membeli motor atau mobil, dan sebagainya. Program ini membantu pengguna menganalisis setiap pilihan secara objektif berdasarkan keuntungan (Benefit) dan kerugian (Cost) yang dimiliki masing-masing pilihan.
 
Setiap Benefit dan Cost memiliki:
- **Value (1-5)** — seberapa menguntungkan atau merugikan faktor tersebut
- **Probability (0.0-1.0)** — seberapa besar kemungkinan faktor tersebut terjadi
 
Skor akhir tiap pilihan dihitung dari: `Σ(value × probability)` untuk Benefit dikurangi `Σ(value × probability)` untuk Cost. Pilihan dengan skor tertinggi akan direkomendasikan oleh sistem.

## Class Diagram
<img width="6929" height="1929" alt="Animal Classification Model-2026-03-25-051631" src="https://github.com/user-attachments/assets/ed4ba173-6d28-4391-87ea-a966bde0b2e2" />

## Kode program
```java
import java.util.ArrayList;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) throws Exception {
        Scanner scan = new Scanner (System.in);
        FinalDecision fd = new FinalDecision();

        System.out.println("Haii, Selamat datang di Decision Maker!!!\n");
        System.out.println("Program ini ditujukan untuk pengguna yang memiliki kebingungan dalam memilih pilihan");
        System.out.println("Keputusan yang disarankan dari sistem berdasarkan aturan Cost and Benefit.");
        System.out.println("Jadi setiap pilihan pastinya memiliki Cost dan Benfit yang didapat, lalu setiap cost atau benefit mempunyai:\n ");                   
        System.out.println("1. Value(harga): Berikan rentang 1-5 [bilangan bulat] berdasarkan seberapa menguntungkan(benefit)/merugikan(cost) sekali hal tersebut bagimu");
        System.out.println("2. Probabilty(kemungkinan): Berikan rentang 0-1 [bilangan desimal] berdasarkan seberapa mungkin cost/benefit itu terjadi\n");

        System.out.println("Sebagai contoh, dalam kasus memilih antara tetap di kampus saat ini VS ikut UTBK lagi, pilihan ikut UTBK lagi memiliki benefit berupa biaya yang lebih terjangkau (value=5, probability=1.0)\n" +
                            "value faktor biaya terjangkau =5 karena semenguntungkan itu masalah biaya bagimu, probability 1 sebab sudah pasti terjadi\n" +
                            "sebaliknya pindah kampus juga memiliki cost seperti mengulang lagi 1 tahun (value=1, probability=1.0), kamu memberikan value 1 karena kamu tidak merasa rugi jika kamu mengulang kembali.\n" + 
                            "Program akan menghitung total dari setiap pilihan dan merekomendasikan pilihan dengan nilai tertinggi dari Benefit - Cost\n");

        System.out.println("Berapa pilihan yang ingin kamu bandingkan? ");
        int jumlahPilihan =scan.nextInt();
        scan.nextLine();

        for (int i = 0; i < jumlahPilihan; i++) {
            System.out.println("Masukkan pilihan "+ (i+1)+ ": " );
            String namaPilihan =scan.nextLine();
            Option myOption = new Option(namaPilihan);

            System.out.print("Berapa benefit yang ingin dimasukkan? ");
            int jumlahBenefit = scan.nextInt();
            scan.nextLine();

            for (int j = 0; j < jumlahBenefit; j++) {
                System.out.print("Deskripsi benefit " + (j+1)+ ": " );
                String desc = scan.nextLine();
                System.out.print("Value, seberapa menguntungkan bagimu (1-5): ");
                int val = scan.nextInt();
                scan.nextLine();
                System.out.print("Probability (0-1): ");
                double prob = scan.nextDouble();
                scan.nextLine();
                myOption.addFaktor(new Benefit(desc, val, prob));
                // make object, n myOption will overwirte evertytime make a new object 
            }
            System.out.print("Berapa cost yang ingin dimasukkan? ");
            int jumlahCost = scan.nextInt();
            scan.nextLine();
            
            for (int j = 0; j < jumlahCost; j++) {
                System.out.print("Deskripsi cost " + (j+1)+ ": " );
                String desc = scan.nextLine();
                System.out.print("Value,sebarapa rugi bagimu (1-5): ");
                int val = scan.nextInt();
                scan.nextLine();
                System.out.print("Probability (0-1): ");
                double prob = scan.nextDouble();
                scan.nextLine();
                myOption.addFaktor(new Cost(desc, val, prob));
            }
            fd.addOption(myOption);
        }


        fd.displayDecision();

    }
}
abstract class Faktor {
    protected String description;
    protected int value;
    protected double probability;

    // constructor
    public Faktor (String description, int value, double probability){
        this.description = description;
        this.value =value;
        this.probability = probability;
    } 

    // setter 
    public void setDescription(String descriptionNew){
        this.description =descriptionNew;
    }
    public void setValue(int valueNew){
        this.value =valueNew;
    }
    public void setProbability(double probabilityNew){
        this.probability =probabilityNew;
    }
    // getter
    public String getDescription (){
        return description;
    }
    public int getValue (){
        return value;
    }
    public double getProbability (){
        return probability;
    }

    abstract double calculateValueProb();
}

class Cost extends Faktor{
    public Cost (String description, int value, double probability){
        super(description, value, probability);
    }

        @Override
        double calculateValueProb(){
            return -(value*probability);
        }
}

class Benefit  extends Faktor{
    public Benefit (String description, int value, double probability){
        super(description, value, probability);
    }

        @Override
        double calculateValueProb(){
            return (value*probability);
        }
}

class Option {


    private String optionName;
    private ArrayList<Faktor> daftarFaktor;

    // constructor
    public Option (String optrionName) {
        this.optionName=optrionName;
        this.daftarFaktor = new ArrayList<>();
    }
    
    public String getOptionName() {
        return optionName;
    }
    public double hitungTotalFaktor(){
        double total = 0; 
        
        for (Faktor i : daftarFaktor) {
            total = total + i.calculateValueProb(); 
        } 

        return total;
    }
    
    public void displaySummary(){
        System.out.println(optionName);

        for (Faktor i : daftarFaktor){
            System.out.println("- "+i.getDescription()+"=" +i.getValue()+" x "+i.getProbability());
        }
        
        System.out.println("Total: " + hitungTotalFaktor()+ "\n");
    }

        public void addFaktor(Faktor f) {
        daftarFaktor.add(f);
    }
}

class FinalDecision {

    private ArrayList<Option> daftarOption;

    public FinalDecision(){
        this.daftarOption = new ArrayList<>();
    }

    public void displayDecision(){
        Option bestOption= daftarOption.get(0);
        for (int i =0; i < daftarOption.size();i++) {
            daftarOption.get(i).displaySummary();
            if (daftarOption.get(i).hitungTotalFaktor()>bestOption.hitungTotalFaktor()) bestOption =daftarOption.get(i); 
        }

        System.out.println("Maka keputusan terbaik bedasarakan Cost Benefit Analisis untukmu adalah " + bestOption.getOptionName());
        System.out.println("Semangat!!!");
    }

    public void addOption(Option o) {
    daftarOption.add(o);
    }
}

```
## Screenshot output
### Pedoman awal program
<img width="1722" height="328" alt="Screenshot 2026-03-25 123619" src="https://github.com/user-attachments/assets/3aedcab1-20f1-4755-89eb-d18bec620955" />

### Tampilan input dari user
<img width="563" height="741" alt="Screenshot 2026-03-25 114432" src="https://github.com/user-attachments/assets/29ab982d-24d9-41dc-9333-71a9d00194fb" />

### Hasil
<img width="989" height="392" alt="Screenshot 2026-03-25 114355" src="https://github.com/user-attachments/assets/c7dedb41-8418-40db-bbad-235ad1300a1d" />

## Penerapan Prinsip OOP
 
1. Abstraction
Class `Faktor` merupakan abstract class yang mendefinisikan kerangka umum dari sebuah faktor keputusan. Method `calculateValueProb()` bersifat abstract karena implementasinya berbeda antara Benefit dan Cost.
 
2. Inheritance
Class `Benefit` dan `Cost` mewarisi class `Faktor`, sehingga tidak perlu mendefinisikan ulang atribut seperti `description`, `value`, dan `probability`.
 
3. Polymorphism
Method `calculateValueProb()` di-override oleh `Benefit` dan `Cost` dengan perilaku berbeda — Benefit mengembalikan nilai positif, Cost mengembalikan nilai negatif. Keduanya diperlakukan seragam sebagai `Faktor` di dalam `ArrayList<Faktor>`.
 
4. Encapsulation
Atribut di setiap class dideklarasikan `private` atau `protected` dan hanya dapat diakses melalui getter dan setter yang disediakan.

## Keunikan 
Program ini tidak sekadar membandingkan pilihan secara sederhana. Setiap faktor memiliki **bobot probabilitas** yang mencerminkan ketidakpastian dunia nyata. Misalnya, benefit "diterima PTN top 3" bernilai tinggi, namun jika probabilitasnya rendah (0.2), kontribusinya terhadap keputusan akhir tetap kecil. Pendekatan ini membuat analisis lebih realistis dibandingkan hanya menjumlahkan nilai mentah tanpa mempertimbangkan kemungkinan terjadinya suatu faktor. Ide program ini terinspirasi dari buku 'Makanya, Mikir!' karya Cania Citta dan Abigail Limuria. Buku tersebut membuka perspektif baru bahwa keputusan sehari-hari, sekecil apapun, dapat dianalisis secara rasional dan terukur.
