# Llama 2

Büyük dil modellerinin gücünü açığa çıkarıyoruz. Llama'nın en son sürümü artık bireyler, yaratıcılar, araştırmacılar ve her ölçekteki işletmeler tarafından kullanılabilmektedir. Bu sayede fikirlerini sorumlulukla deneyimleyebilir, yenilik yapabilir ve ölçeklendirebilirler.

Bu sürüm, önceden eğitilmiş ve ince ayarlı Llama dil modelleri için model ağırlıklarını ve başlangıç kodunu içermektedir - 7B'den 70B parametreye kadar.

Bu depo, [Llama 2](https://ai.meta.com/research/publications/llama-2-open-foundation-and-fine-tuned-chat-models/) modellerini yüklemek ve çıkarım yapmak için minimal bir örnek olarak tasarlanmıştır. Daha detaylı HuggingFace örnekleri için [llama-recipes](https://github.com/facebookresearch/llama-recipes/) sayfasına bakabilirsiniz.

## İndirme

⚠️ **7/18: Bugün birçok indirme sorunu yaşayan insanların farkındayız. Hala sorun yaşayanlar tüm yerel dosyaları kaldırmalı, depoyu yeniden klonlamalı ve [yeni bir indirme bağlantısı istemelidir](https://ai.meta.com/resources/models-and-libraries/llama-downloads/). Yerel bozuk dosyalarınız varsa, bunları düzeltmek kritik öneme sahiptir. E-postayı aldığınızda, sadece link metnini kopyalayın - link, https://download.llamameta.net ile başlamalı ve hatalar veren https://l.facebook.com ile başlamamalıdır.**

Model ağırlıklarını ve belirteci (tokenizer) indirmek için, lütfen [Meta AI web sitesini](https://ai.meta.com/resources/models-and-libraries/llama-downloads/) ziyaret edin ve lisansımızı kabul edin.

Talebiniz onaylandığında, e-posta yoluyla imzalanmış bir URL alacaksınız. Ardından `download.sh` betiğini çalıştırarak indirmeyi başlatmak için sağlanan URL'yi geçirin. URL metnini kendiniz kopyaladığınızdan emin olun, URL'yi sağ tıklayıp "Bağlantı adresini kopyala" seçeneğini kullanmayın. Kopyalanan URL metni https://download.llamameta.net ile başlıyorsa, doğru şekilde kopyalamışsınız demektir. Eğer kopyalanan URL metni https://l.facebook.com ile başlıyorsa, yanlış şekilde kopyalamışsınız demektir.

Ön koşullar: `wget` ve `md5sum` kurulu olduğundan emin olun. Ardından betiği çalıştırmak için: `./download.sh`.

Unutmayın ki, bağlantılar 24 saat veya belli bir sayıda indirme sonrasında süresi dolmaktadır. "403: Yasaklı" gibi hatalar görmeye başlarsanız, her zaman yeni bir bağlantı isteyebilirsiniz.

### Hugging Face Erişimi

Ayrıca, [Hugging Face](https://huggingface.co/meta-llama) üzerinden indirmeler sağlıyoruz. Hugging Face hesabınızın e-posta adresini kullanarak Meta AI web sitesinden indirme isteği yapmanız gerekmektedir. Ardından Hugging Face üzerinden istediğiniz herhangi bir modele erişim talep edebilir ve 1-2 gün içinde hesabınıza tüm sürümler için erişim verilecektir.

## Kurulum

PyTorch / CUDA desteği olan bir conda ortamında, depoyu klonlayın ve üst düzey dizinde şunu çalıştırın:

```
pip install -e .
```

## Çıkarım (Inference)

Farklı modeller, farklı model-paralel (MP) değerleri gerektirir:

| Model | MP |
|--------|----|
| 7B     | 1  |
| 13B    | 2  |
| 70B    | 8  |

Tüm modeller, 4096 belirtece kadar uzunluğa sahip dizileri destekler, ancak önbelleği `max_seq_len` ve `max_batch_size` değerlerine göre önceden ayırmaktayız. Bu nedenle donanımınıza uygun şekilde bu değerleri ayarlayın.

### Önceden Eğitilmiş Modeller

Bu modeller sohbet veya soru-cevap için ince ayarlanmamıştır. Sorunun doğal bir devamı olarak beklenen cevabın elde edilmesi için uygun şekilde yönlendirilmelidirler.

Bazı örnekler için `example_text_completion.py` dosyasına bakabilirsiniz. İllüstrasyon için, aşağıdaki komutu kullanarak llama-2-7b modeliyle çalıştırabilirsiniz (`nproc_per_node` değeri, `MP` değerine ayarlanmalıdır):

```
torchrun --nproc_per_node 1 example_text_completion.py \
    --ckpt_dir llama-2-7b/ \
    --tokenizer_path tokenizer.model \
    --max_seq_len 128 --max_batch_size 4
```

### İnce Ayarlanmış Sohbet Modelleri

İnce ayarlanmış modeller, diyalog uygulamaları için eğitilmiştir. Onlardan beklenen özellikleri ve performansı elde etmek için, [`chat_completion`](https://github.com/facebookresearch/llama/blob/main/llama/generation.py#L212) adlı özel bir biçim kullanılmalıdır. Bu biçimde `INST` ve `<<SYS>>` etiketleri, `BOS` ve `EOS` belirteçleri ve bunların arasındaki boşluklar ve satır sonları bulunmaktadır (çift bo

şluklardan kaçınmak için girişlere `strip()` yöntemi uygulamak önerilir).

Ayrıca, giriş ve çıkışlardan güvenli olmayan içerikleri filtrelemek için ek sınıflandırıcılar da ekleyebilirsiniz. Girişlerin ve çıkışların güvenli olduğunu kontrol etmek için llama-recipes deposunda [bir örnek](https://github.com/facebookresearch/llama-recipes/blob/main/inference/inference.py) bulunmaktadır.

llama-2-7b-chat kullanarak örnekler:

```
torchrun --nproc_per_node 1 example_chat_completion.py \
    --ckpt_dir llama-2-7b-chat/ \
    --tokenizer_path tokenizer.model \
    --max_seq_len 512 --max_batch_size 4
```

Llama 2, kullanımı potansiyel riskler taşıyan yeni bir teknolojidir. Şu ana kadar yapılan testler tüm senaryoları kapsayamamıştır ve kapsayamayacaktır.
Geliştiricilerin bu riskleri ele almalarına yardımcı olmak için [Sorumlu Kullanım Kılavuzu](Responsible-Use-Guide.pdf) oluşturduk. Daha fazla ayrıntı için araştırma makalemizi inceleyebilirsiniz.

## Sorunlar (Issues)

Modellerle ilgili herhangi bir yazılım hatası veya diğer sorunları aşağıdaki yollardan biriyle bildirebilirsiniz:
- Modelle ilgili sorunları bildirme: [github.com/facebookresearch/llama](http://github.com/facebookresearch/llama)
- Model tarafından üretilen riskli içeriği bildirme: [developers.facebook.com/llama_output_feedback](http://developers.facebook.com/llama_output_feedback)
- Yazılım hataları ve güvenlik endişeleri bildirme: [facebook.com/whitehat/info](http://facebook.com/whitehat/info)

## Model Kartı (Model Card)

[MODEL_CARD.md](MODEL_CARD.md) dosyasına bakabilirsiniz.

## Lisans (License)

Model ve ağırlıkları, araştırmacılar ve ticari kuruluşlar için lisanslıdır ve açıklık prensiplerini korur. Misyonumuz, bu fırsatlar aracılığıyla bireyleri ve endüstriyi güçlendirmek ve etik yapay zeka gelişimine katkıda bulunmaktır.

[LICENSE](LICENSE) dosyasını ve beraberindeki [Kabul Edilebilir Kullanım Politikası](USE_POLICY.md) belgesini inceleyebilirsiniz.

## Referanslar (References)

1. [Araştırma Makalesi](https://ai.meta.com/research/publications/llama-2-open-foundation-and-fine-tuned-chat-models/)
2. [Llama 2 Teknik Genel Bakış](https://ai.meta.com/resources/models-and-libraries/llama)
3. [Açık İnovasyon Yapay Zeka Araştırma Topluluğu](https://ai.meta.com/llama/open-innovation-ai-research-community/)

## Orijinal LLaMA

Orijinal Llama sürümüne ait depo, [`llama_v1`](https://github.com/facebookresearch/llama/tree/llama_v1) dalında bulunmaktadır.
