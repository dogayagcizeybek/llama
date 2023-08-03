# **Model Detayları**

Meta, büyük dil modelleri (LLM'ler) ailesi olan Llama 2'yi geliştirdi ve yayınladı. Bu koleksiyon, 7 milyar ila 70 milyar parametreye kadar ölçeklenebilen, önceden eğitilmiş ve ince ayarlı üretken metin modellerinden oluşur. İnce ayarlı Llama-2-Chat modelleri, diyalog kullanım durumları için optimize edilmiştir. Llama-2-Chat modelleri, test ettiğimiz çoğu açık kaynaklı sohbet modelini geride bırakır ve yardımseverlik ve güvenlik için insan değerlendirmelerimizde, ChatGPT ve PaLM gibi bazı popüler kapalı kaynaklı modellerle eşdeğerdir.

**Model Geliştiricileri:** Meta

**Çeşitlilikler:** Llama 2, 7B, 13B ve 70B olmak üzere farklı parametre boyutlarında ve önceden eğitilmiş ve ince ayarlı çeşitliliklerde gelir.

**Girdi:** Modeller yalnızca metin girişi alır.

**Çıktı:** Modeller yalnızca metin üretir.

**Model Mimarisi:** Llama 2, optimize edilmiş bir dönüşümcü mimari kullanan otoregresif bir dil modelidir. Ayarlanmış sürümler, yardımseverlik ve güvenlik için insan tercihlerine uyum sağlamak için gözetimli ince ayar (SFT) ve insan geri bildirimiyle pekiştirmeli öğrenme (RLHF) kullanır.

| |Eğitim Verisi|Parametreler|İçerik Uzunluğu|GQA|Belirteçler|LR|
|---|---|---|---|---|---|---|
Llama 2|*Kamuoyunda mevcut çevrimiçi verilerin yeni bir karışımı*|7B|4k|&#10007;|2.0T|3.0 x 10<sup>-4</sup>
Llama 2|*Kamuoyunda mevcut çevrimiçi verilerin yeni bir karışımı*|13B|4k|&#10007;|2.0T|3.0 x 10<sup>-4</sup>
Llama 2|*Kamuoyunda mevcut çevrimiçi verilerin yeni bir karışımı*|70B|4k|&#10004;|2.0T|1.5 x 10<sup>-4</sup>

**Llama 2 modellerinin aileleri.** Belirteç sayıları yalnızca ön eğitim verilerine göre verilmiştir. Tüm modeller, global bir parti boyutu olan 4M belirteçle eğitilmiştir. 70B sürümü, daha iyi çıkarım ölçeklenebilirliği için Gruplu-Sorgu Dikkati (GQA) kullanır.

**Model Tarihleri:** Llama 2, 2023 yılı Ocak ve Temmuz ayları arasında eğitilmiştir.

**Durum:** Bu, çevrimdışı bir veri kümesi üzerinde eğitilmiş statik bir modeldir. Topluluk geri bildirimiyle model güvenliğini iyileştirdikçe, ayarlanmış modellerin gelecekteki sürümleri yayınlanacaktır.

**Lisans:** Özel bir ticari lisans, şuradan temin edilebilir: [https://ai.meta.com/resources/models-and-libraries/llama-downloads/](https://ai.meta.com/resources/models-and-libraries/llama-downloads/)

**Araştırma Makalesi:** Daha fazla bilgi için "Llama-2: Açık Temel ve İnce Ayarlı Sohbet Modelleri" başlıklı makaleye, şu adresten ulaşılabilir: [https://ai.meta.com/research/publications/llama-2-open-foundation-and-fine-tuned-chat-models/](https://ai.meta.com/research/publications/llama-2-open-foundation-and-fine-tuned-chat-models/).

**Model hakkındaki soruları veya yorumları nereye göndermek için** Modelle ilgili geri bildirim veya yorumları sağlama talimatları, model [README](README.md) dosyasında bulunabilir.

# **Amaçlanan Kullanım**
**Amaçlanan Kullanım Durumları** Llama 2, İngilizce olarak ticari ve araştırma amaçları için tasarlanmıştır. Ayarlanmış modeller, asistan benzeri sohbet için tasarlanmışken, önceden eğitilmiş modeller çeşitli doğal dil üretimi görevlerine uygun olarak adapte edilebilir.

**Kapsam Dışı Kullanımlar** Geçerli yasalara veya düzenlemelere aykırı şekilde kullanmak. İngilizce dışında dillerde kullanmak. Llama 2 için Kabul Edilebilir Kullanım Politikası ve Lisans Anlaşması tarafından yasaklanmış başka bir şekilde kullanmak.

# **Donanım ve Yazılım**
**Eğitim Faktörleri** Ön eğitimde özel eğitim kitaplıkları, Meta'nın Araştırma Süper Kümesi ve ön eğitim için üretim kümeleri kullanılmıştır. İnce ayar, işaretleme ve değerlendirme işlemleri üçüncü taraf bulut hesaplamasında gerçekleştirilmiştir.

**Karbon Ayakizi** Ön eğitimde, ortalama 3.3M GPU saati, 350-400W TDP'li A100-80GB türündeki donanımlarda hesaplanmıştır. Tahmini toplam emisyon 539 tCO2eq idi ve bu emisyonların tamamı Meta'nın sürdürülebilirlik programı tarafından telafi edilmiştir

.

||Süre (GPU saat)|Güç Tüketimi (W)|Emisyon (tCO<sub>2</sub>eq)|
|---|---|---|---|
|Llama 2 7B|184320|400|31.22|
|Llama 2 13B|368640|400|62.44|
|Llama 2 70B|1720320|400|291.42|
|Toplam|3311616||539.00|

**Ön eğitim sırasında CO<sub>2</sub> emisyonları.** Süre: her modelin eğitimi için gereken toplam GPU süresi. Güç Tüketimi: kullanılan GPU'lar için tepe güç kapasitesi ve güç kullanım verimliliği için düzeltilmiş değer. Emisyonların %100'ü doğrudan Meta'nın sürdürülebilirlik programı tarafından telafi edilmiştir ve bu modelleri açıkça yayınladığımızdan dolayı, ön eğitim maliyetleri diğerlerinin tarafından karşılanmak zorunda değildir.

# **Eğitim Verisi**
**Genel Bakış** Llama 2, kamuoyunda mevcut kaynaklardan 2 trilyon belirteçlik veri üzerinde ön eğitimden geçirilmiştir. İnce ayar verileri, kamuoyunda mevcut talimat veri kümesi ile birlikte bir milyondan fazla yeni insan tarafından belirtilmiş örnek içerir. Ne ön eğitim veri kümesi ne de ince ayar veri kümesi, Meta kullanıcı verilerini içerir.

**Veri Tazeliği** Ön eğitim verilerinin kesim tarihi 2022 yılı Eylül ayına kadar, ancak bazı ayarlama verileri daha yeni, 2023 Temmuz ayına kadar olan verileri içerir.

# **Değerlendirme Sonuçları**

Bu bölümde, Llama 1 ve Llama 2 modellerinin standart akademik değerlendirme kriterlerindeki sonuçlarını rapor ediyoruz. Tüm değerlendirmeler için, iç değerlendirme kitaplığımızı kullanıyoruz.

|Model|Boyut|Kod|Sağduyu Çıkarımı|Dünya Bilgisi|Okuma Anlama|Matematik|MMLU|BBH|AGI Değerlendirmesi|
|---|---|---|---|---|---|---|---|---|---|
|Llama 1|7B|14.1|60.8|46.2|58.5|6.95|35.1|30.3|23.9|
|Llama 1|13B|18.9|66.1|52.6|62.3|10.9|46.9|37.0|33.9|
|Llama 1|33B|26.0|70.0|58.4|67.6|21.4|57.8|39.8|41.7|
|Llama 1|65B|30.7|70.7|60.5|68.6|30.8|63.4|43.5|47.6|
|Llama 2|7B|16.8|63.9|48.9|61.3|14.6|45.3|32.6|29.3|
|Llama 2|13B|24.5|66.9|55.4|65.8|28.7|54.8|39.4|39.1|
|Llama 2|70B|**37.5**|**71.9**|**63.6**|**69.4**|**35.2**|**68.9**|**51.2**|**54.2**|

**Gruplanmış akademik değerlendirme kriterlerinde genel performans.** *Kod:* Modellerimizin HumanEval ve MBPP üzerindeki ortalama geçiş@1 puanlarını rapor ediyoruz. *Sağduyu Çıkarımı:* PIQA, SIQA, HellaSwag, WinoGrande, ARC kolay ve zor, OpenBookQA ve CommonsenseQA'nın 7-shot sonuçlarını ve diğer tüm kriterler için 0-shot sonuçlarını rapor ediyoruz. *Dünya Bilgisi:* NaturalQuestions ve TriviaQA üzerindeki 5-shot performansını değerlendiriyoruz ve ortalama sonuçlarını rapor ediyoruz. *Okuma Anlama:* Okuma anlama için SQuAD, QuAC ve BoolQ'daki 0-shot ortalama sonuçlarını rapor ediyoruz. *MATEMATİK:* GSM8K (8 atış) ve MATH (4 atış) kriterlerinin en üst düzeydeki sonuçlarını rapor ediyoruz.

|||TruthfulQA|Toxigen|
|---|---|---|---|
|Llama 1|7B|27.42|23.00|
|Llama 1|13B|41.74|23.08|
|Llama 1|33B|44.19|22.57|
|Llama 1|65B|48.71|21.77|
|Llama 2|7B|33.29|**21.25**|
|Llama 2|13B|41.86|26.10|
|Llama 2|70B|**50.18**|24.60|

**Önceden eğitilmiş LLM'lerin otomatik güvenlik değerlendirmeleri.** TruthfulQA için, doğru ve bilgi içeren nesillerin yüzdesini sunuyoruz (yüzde ne kadar yüksekse o kadar iyi). ToxiGen için, toksik nesillerin yüzdesini sunuyoruz (yüzde ne kadar düşükse o kadar iyi).

|||TruthfulQA|Toxigen|
|---|---|---|---|
|Llama-2-Chat|7B|57.04|**0.00**|
|Llama-2-Chat|13B|62.18|**0.00**|
|Llama-2-Chat|70B|**64.14**|0.01|

**Ayarlanmış LLM'lerin

 farklı güvenlik veri kümeleri üzerinde değerlendirmesi.** Yukarıdaki metrik tanımlamaları ile aynıdır.

# **Etik Düşünceler ve Sınırlamalar**
Llama 2, kullanımıyla birlikte riskler taşıyan yeni bir teknolojidir. Şu ana kadar yapılan testler İngilizce dilinde gerçekleştirilmiş olup tüm senaryoları kapsamamıştır ve kapsayamayabilir. Bu nedenlerle, tıpkı tüm LLM'ler gibi, Llama 2'nin potansiyel çıktıları önceden tahmin edilemez ve model, bazı durumlarda kullanıcı taleplerine yanlış, önyargılı veya başka sakıncalı yanıtlar verebilir. Bu nedenle, Llama 2'nin herhangi bir uygulamasını yayınlamadan önce, geliştiriciler, modelin özgün uygulamalarına yönelik güvenlik testleri ve ayarlamaları yapmalıdır.

Lütfen Sorumlu Kullanım Kılavuzunu şu adresten inceleyin: [https://ai.meta.com/llama/responsible-use-guide/](https://ai.meta.com/llama/responsible-use-guide/)