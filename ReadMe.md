# The Cashier
The cashier adalah program kasir sederhana yang datanya bersifat sementara dan digunakan untuk mendata transaksi dalam jangka waktu satu hari saja.

### Cara Menggunakan
- Input data-data pada form Cashier
- Setelah Menginputkan klik tombol "Tambahkan"
- Setelah itu lihat hasil-nya pada bagian ListBox dan Total

### Kelebihan & Kekurangan
#### - Kelebihan
- Simpel dan mudah dimengerti
- Data yang diinputkan menjadi lebih jelas
- Hasil langsung dilihatkan dengan valid 100%

#### - Kekurangan 
- Data tidak permanen
- Jika program keluar data hilang
- Hanya bisa digunakan untuk menghitung jangka pendek

### Penjelasan Koding
Pada program ini saya menggunakan dua Class tambahan yang pertama digunakan untuk deklarasi dan hitung dari data, dan yang kedua digunakan untuk menghubungkan data ke-ListBox. Untuk Class pertama saya berinama Class Item dan seperti ini kodingan-nya

     class Item
    {
        private int id;
        public string title { get; set; }
        public int quantity { get; set; }
        public double price { get; set; }
        public double subtotal { get; set; }
        private string type;

        public Item(int id, string title, int quantity, double price, double subtotal, string type)
        {
            this.id = id;
            this.title = title;
            this.quantity = quantity;
            this.price = price;
            this.subtotal = subtotal;
            this.type = type;
        }

        public string getTitle()
        {
            return title;
        }
        public int getQuantity()
        {
            return quantity;
        }
        public string getType()
        {
            return type;
        }
        public double getPrice()
        {
            return price;
        }
        public double getSubTotal()
        {
            subtotal = price * quantity;
            return subtotal;
        }
    }

Pada bagian atas Class Item adalah deklarasi dari variable yang dibutuhkan, dan bagian tengah ke-bawah adalah pengambilan nilai dari variable. Pada Class Item ini ada satu perhitungan dengan koding seperti ini

    public double getSubTotal()
        {
            subtotal = price * quantity;
            return subtotal;
        }

Pada Bagian ini adalah perhitungan dari Nilai price dikali Nilai quantity dan hasilnya dimasukkan ke dalam varibale subtotal. Dan Untuk Class Kedua  saya berinama Class  Calculator dan seperti ini kodingan-nya

    class Calculator
    {
        private List<Item> listItem;
        private double total = 0;
        
        public Calculator()
        {
            this.listItem = new List<Item>();
        }
        public void addItem(Item item)
        {
            this.listItem.Add(item);
            this.total += item.getSubTotal();
        }
        public double getTotal()
        {
            return total;
        }
        public List<Item> getListItem()
        {
            return listItem;
        }
    }

Pada bagian atas pada Class ini digunakan untuk deklarasi atau digunakan untuk menghubungkan Class Item, dan bagian bawah-nya digunakan untuk mendapatkan atau mengambil nilai dari Class Item dan Variable lain. Di Class ini ada perhitungan dengan kodingan seperti ini 

    public void addItem(Item item)
        {
            this.listItem.Add(item);
            this.total += item.getSubTotal();
        }

Artinya adalah dari list Item atau dari Class Item, varibale total akan ditambah dengan item.getSubTotal dan dimasukkan lagi ke varibale total. Setelah dari Class Calculator maka kita akan kembali ke Class Pertama dengan koding seperti ini

    public partial class MainWindow : Window
    {
        private Calculator calculator;
        public MainWindow()
        {
            InitializeComponent();
            calculator = new Calculator();
            listBox.ItemsSource = calculator.getListItem();
        }

        private void addButton_Click(object sender, RoutedEventArgs e)
        {
            string title = itemNameBox.Text;
            int quantity = int.Parse(quantityBox.Text);
            string type = typeBox.Text;
            double price = double.Parse(priceBox.Text);

            Item item = new Item(new Random().Next(), title, quantity, price, price, type);
            calculator.addItem(item);
            double total = calculator.getTotal();

            totalLabel.Content = string.Format("Rp. {0}", total);

            listBox.Items.Refresh();

            itemNameBox.Text = "";
            quantityBox.Text = "";
            typeBox.Text = "";
            priceBox.Text = "";
            itemNameBox.Focus();
        }
    }

Pada Bagian atas berfungsi untuk memanggil Class Calculator yang sudah terhubung dengan Class Item tadi, pada bagian tengah atau bagian addButton kita harus mendeklarasikan Box-Box pada form dengan tipe varible yang disesuaikan dengan Class Item. Pada bagian tengah atau bagian untuk menampilkan berada dan berpusat pada bagian 

    Item item = new Item(new Random().Next(), title, quantity, price, price, type);
            calculator.addItem(item);
            double total = calculator.getTotal();

            totalLabel.Content = string.Format("Rp. {0}", total);

            listBox.Items.Refresh();

Dengan begitu selesai sudah Kodingan penting pada program ini dan pada bagian paling terakhir adalah 

    itemNameBox.Text = "";
    quantityBox.Text = "";
    typeBox.Text = "";
    priceBox.Text = "";
    itemNameBox.Focus();

Kodingan ini digunakan untuk merapikan tampilan setelah menginputkan data pada form Cashier.