import 'package:flutter/material.dart';
import 'package:url_launcher/url_launcher.dart';

void main() {
  runApp(const SouqArtiApp());
}

class SouqArtiApp extends StatelessWidget {
  const SouqArtiApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'سوق آرتي',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        brightness: Brightness.dark,
        scaffoldBackgroundColor: const Color(0xFF0B132B),
        appBarTheme: const AppBarTheme(
          backgroundColor: Color(0xFF0B132B),
          centerTitle: true,
        ),
      ),
      home: const HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  const HomeScreen({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return DefaultTabController(
      length: 2,
      child: Scaffold(
        appBar: AppBar(
          title: const Text('سوق آرتي', style: TextStyle(color: Color(0xFFFFD700), fontWeight: FontWeight.bold)),
          bottom: const TabBar(
            indicatorColor: Color(0xFFFFD700),
            labelColor: Color(0xFFFFD700),
            unselectedLabelColor: Colors.white60,
            tabs: [
              Tab(icon: Icon(Icons.store), text: 'لوحة التاجر'),
              Tab(icon: Icon(Icons.phonelink_setup), text: 'طلب استبدال'),
            ],
          ),
        ),
        body: const TabBarView(
          children: [
            MerchantUploadScreen(),
            ReplacementRequestScreen(),
          ],
        ),
      ),
    );
  }
}

class MerchantUploadScreen extends StatefulWidget {
  const MerchantUploadScreen({Key? key}) : super(key: key);

  @override
  State<MerchantUploadScreen> createState() => _MerchantUploadScreenState();
}

class _MerchantUploadScreenState extends State<MerchantUploadScreen> {
  final _phoneNameController = TextEditingController();
  final _priceController = TextEditingController();
  bool _goldenGuarantee = true;

  @override
  void dispose() {
    _phoneNameController.dispose();
    _priceController.dispose();
    super.dispose();
  }

  void _publishProduct() {
    String name = _phoneNameController.text.trim();
    String price = _priceController.text.trim();

    if (name.isEmpty || price.isEmpty) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('الرجاء إدخال اسم الهاتف والسعر')),
      );
      return;
    }

    ScaffoldMessenger.of(context).showSnackBar(
      SnackBar(content: Text('تم نشر الهاتف ($name) بنجاح مع الضمان الذهبي!')),
    );

    _phoneNameController.clear();
    _priceController.clear();
  }

  @override
  Widget build(BuildContext context) {
    return SingleChildScrollView(
      padding: const EdgeInsets.all(16.0),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Container(
            height: 180,
            width: double.infinity,
            decoration: BoxDecoration(
              color: Colors.black,
              borderRadius: BorderRadius.circular(15),
              border: Border.all(color: const Color(0xFFFFD700), width: 2),
            ),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: const [
                Icon(Icons.camera, size: 50, color: Color(0xFFFFD700)),
                SizedBox(height: 10),
                Text('كاميرا التاجر المباشرة لالتقاط صورة الهاتف', style: TextStyle(color: Colors.white70, fontSize: 14)),
              ],
            ),
          ),
          const SizedBox(height: 20),
          TextField(
            controller: _phoneNameController,
            style: const TextStyle(color: Colors.white),
            decoration: InputDecoration(
              labelText: 'اسم الهاتف ومواصفاته',
              labelStyle: const TextStyle(color: Colors.white70),
              enabledBorder: OutlineInputBorder(
                borderSide: const BorderSide(color: Color(0xFF00FFFF)),
                borderRadius: BorderRadius.circular(10),
              ),
              focusedBorder: OutlineInputBorder(
                borderSide: const BorderSide(color: Color(0xFFFFD700), width: 2),
                borderRadius: BorderRadius.circular(10),
              ),
            ),
          ),
          const SizedBox(height: 20),
          TextField(
            controller: _priceController,
            keyboardType: TextInputType.number,
            style: const TextStyle(color: Colors.white),
            decoration: InputDecoration(
              labelText: 'سعر البيع (ر.ي)',
              labelStyle: const TextStyle(color: Colors.white70),
              enabledBorder: OutlineInputBorder(
                borderSide: const BorderSide(color: Color(0xFF00FFFF)),
                borderRadius: BorderRadius.circular(10),
              ),
              focusedBorder: OutlineInputBorder(
                borderSide: const BorderSide(color: Color(0xFFFFD700), width: 2),
                borderRadius: BorderRadius.circular(10),
              ),
            ),
          ),
          const SizedBox(height: 20),
          Container(
            padding: const EdgeInsets.symmetric(horizontal: 16, vertical: 8),
            decoration: BoxDecoration(
              border: Border.all(color: const Color(0xFFFFD700)),
              borderRadius: BorderRadius.circular(10),
              color: const Color(0xFF1C2541),
            ),
            child: Row(
              mainAxisAlignment: MainAxisAlignment.spaceBetween,
              children: [
                const Text('🌟 تفعيل الضمان الذهبي', style: TextStyle(color: Colors.white, fontSize: 16, fontWeight: FontWeight.bold)),
                Switch(
                  value: _goldenGuarantee,
                  activeColor: const Color(0xFFFFD700),
                  onChanged: (bool value) {
                    setState(() {
                      _goldenGuarantee = value;
                    });
                  },
                ),
              ],
            ),
          ),
          const SizedBox(height: 30),
          SizedBox(
            width: double.infinity,
            height: 50,
            child: ElevatedButton(
              style: ElevatedButton.styleFrom(
                backgroundColor: const Color(0xFFFFD700),
                shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
              ),
              onPressed: _publishProduct,
              child: const Text('تحميل ونشر المنتج فوراً', style: TextStyle(fontSize: 16, color: Colors.black, fontWeight: FontWeight.bold)),
            ),
          ),
        ],
      ),
    );
  }
}

class ReplacementRequestScreen extends StatefulWidget {
  const ReplacementRequestScreen({Key? key}) : super(key: key);

  @override
  State<ReplacementRequestScreen> createState() => _ReplacementRequestScreenState();
}

class _ReplacementRequestScreenState extends State<ReplacementRequestScreen> {
  final _phoneModelController = TextEditingController();
  final _priceDifferenceController = TextEditingController();
  String _selectedCondition = 'ممتاز (بدون خدوش)';

  final List<String> _conditions = [
    'جديد تماماً',
    'ممتاز (بدون خدوش)',
    'مستعمل نظيف',
    'يحتاج صيانة بسيطة'
  ];

  @override
  void dispose() {
    _phoneModelController.dispose();
    _priceDifferenceController.dispose();
    super.dispose();
  }

  Future<void> _sendToWhatsApp() async {
    String model = _phoneModelController.text.trim();
    String diffPrice = _priceDifferenceController.text.trim();

    if (model.isEmpty || diffPrice.isEmpty) {
      ScaffoldMessenger.of(context).showSnackBar(
        const SnackBar(content: Text('الرجاء إدخال نوع الهاتف ومبلغ الفرق المتوقع')),
      );
      return;
    }

    String message = '''طلب استبدال هاتف جديد من تطبيق سوق آرتي:
- نوع الهاتف: $model
- الحالة: $_selectedCondition
- مبلغ الفرق المتوقع: $diffPrice ر.ي''';

    final url = Uri.parse('https://wa.me/967773811111?text=${Uri.encodeComponent(message)}');
    if (await canLaunchUrl(url)) {
      await launchUrl(url, mode: LaunchMode.externalApplication);
    }
  }

  @override
  Widget build(BuildContext context) {
    return SingleChildScrollView(
      padding: const EdgeInsets.all(16.0),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Container(
            height: 180,
            width: double.infinity,
            decoration: BoxDecoration(
              color: const Color(0xFF1C2541),
              borderRadius: BorderRadius.circular(15),
              border: Border.all(color: const Color(0xFF00FFFF), width: 1.5),
            ),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: const [
                Icon(Icons.camera_alt, size: 50, color: Color(0xFF00FFFF)),
                SizedBox(height: 10),
                Text('التقط صورة جهازي الحالي بالكاميرا', style: TextStyle(color: Colors.white, fontSize: 16)),
              ],
            ),
          ),
          const SizedBox(height: 20),
          TextField(
            controller: _phoneModelController,
            style: const TextStyle(color: Colors.white),
            decoration: InputDecoration(
              labelText: 'نوع جهازه والموديل',
              labelStyle: const TextStyle(color: Colors.white70),
              enabledBorder: OutlineInputBorder(
                borderSide: const BorderSide(color: Color(0xFF00FFFF)),
                borderRadius: BorderRadius.circular(10),
              ),
              focusedBorder: OutlineInputBorder(
                borderSide: const BorderSide(color: Color(0xFFFFD700), width: 2),
                borderRadius: BorderRadius.circular(10),
              ),
            ),
          ),
          const SizedBox(height: 20),
          const Text('حالة الجهاز:', style: TextStyle(color: Colors.white70, fontSize: 14)),
          const SizedBox(height: 8),
          Container(
            padding: const EdgeInsets.symmetric(horizontal: 12),
            decoration: BoxDecoration(
              border: Border.all(color: const Color(0xFF00FFFF)),
              borderRadius: BorderRadius.circular(10),
              color: const Color(0xFF1C2541),
            ),
            child: DropdownButtonHideUnderline(
              child: DropdownButton<String>(
                value: _selectedCondition,
                dropdownColor: const Color(0xFF1C2541),
                isExpanded: true,
                style: const TextStyle(color: Colors.white),
                items: _conditions.map((String condition) {
                  return DropdownMenuItem<String>(
                    value: condition,
                    child: Text(condition),
                  );
                }).toList(),
                onChanged: (String? newValue) {
                  setState(() {
                    _selectedCondition = newValue!;
                  });
                },
              ),
            ),
          ),
          const SizedBox(height: 20),
          TextField(
            controller: _priceDifferenceController,
            keyboardType: TextInputType.number,
            style: const TextStyle(color: Colors.white),
            decoration: InputDecoration(
              labelText: 'المبلغ المتوقع لفرق الاستبدال (ر.ي)',
              labelStyle: const TextStyle(color: Colors.white70),
              enabledBorder: OutlineInputBorder(
                borderSide: const BorderSide(color: Color(0xFF00FFFF)),
                borderRadius: BorderRadius.circular(10),
              ),
              focusedBorder: OutlineInputBorder(
                borderSide: const BorderSide(color: Color(0xFFFFD700), width: 2),
                borderRadius: BorderRadius.circular(10),
              ),
            ),
          ),
          const SizedBox(height: 30),
          SizedBox(
            width: double.infinity,
            height: 50,
            child: ElevatedButton(
              style: ElevatedButton.styleFrom(
                backgroundColor: const Color(0xFF25D366),
                shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
              ),
              onPressed: _sendToWhatsApp,
              child: Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: const [
                  Icon(Icons.send, color: Colors.white),
                  SizedBox(width: 8),
                  Text('إرسال طلب الاستبدال', style: TextStyle(fontSize: 16, color: Colors.white, fontWeight: FontWeight.bold)),
                ],
              ),
            ),
          ),
        ],
      ),
    );
  }
}
