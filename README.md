# Kivi 🥝 — Türkçe Müşteri Hizmetleri Asistanı

Kivi, kurgusal Kivi Elektronik mağazası için geliştirilen Türkçe bir yapay zekâ asistanıdır. Ürün bilgileri, sipariş, ödeme, kargo, iade ve garanti konularında destek sağlamayı amaçlar.

Bu proje, bir eğitim programında sağlanan başlangıç defteri temel alınarak Seda Ahi tarafından uyarlanmış ve geliştirilmiştir.

## Nasıl çalışır?

- **QLoRA ince ayarı:** Modelin Kivi kimliğini, üslubunu ve araç kullanma davranışını öğrenmesi için kullanılır.
- **RAG:** Mağaza kuralları, verilen soruyla ilgili rehber bölümleri bulunarak modele aktarılır.
- **Araç kullanımı:** Ürün tablosundan bilgi alma, hesaplama ve kargo ücreti hesaplama işlemleri gerçekleştirilir.

Arayüzde Sohbet, Rehber (RAG) ve Ajan olmak üzere üç mod bulunur.

## Kullanılan teknolojiler

Python, Google Colab, Hugging Face Transformers, PEFT/QLoRA, Chroma, Gradio ve GGUF.

Taban model: `Qwen/Qwen2.5-1.5B-Instruct`

## Veri ve eğitim

- 475 sentetik sohbet örneği
- 428 eğitim, 47 değerlendirme örneği
- Colab T4 GPU üzerinde 3 epoch eğitim
- Rehber belgesi ve ürün tablosu
- Ek geliştirilen `kargo_ucreti` aracı

## Sonuçlar


| Ölçüt                       | Eğitim öncesi | Eğitim sonrası |
| ------------------------------ | --------------: | ---------------: |
| Geçerli ajan JSON çıktısı |            0.81 |             1.00 |
| Doğru araç seçimi           |            0.12 |             0.94 |
| RAG hakem puanı               |            0.47 |             0.53 |

Ayrı olarak uygulanan 15 soruluk uçtan uca testte ortalama puan **0.37** olmuştur. Bu puan, otomatik hakemin verdiği 0, 0.5 ve 1 puanlarının ortalamasıdır; doğruluk yüzdesi olarak yorumlanmamalıdır.

Modelin biçim ve araç seçimi başarısındaki artış, bütün cevapların doğru olduğu anlamına gelmez.

## Sınırlamalar

Bu çalışma eğitim amaçlı bir prototiptir ve gerçek müşteri sistemlerine bağlı değildir.

Model, rehber sağlansa bile koşulları atlayabilir, çelişkili cevaplar verebilir veya kaynakta bulunmayan bilgiler üretebilir. Birden fazla araç gerektiren işlemlerde adım atlayabilir.

## Proje dosyaları

- `notebooks/kivi-assistant.ipynb`: Eğitim, değerlendirme ve uygulama adımlarını içeren Colab defteri.
- `.gitignore`: Yerel ayarların, gizli dosyaların ve büyük model dosyalarının Git'e eklenmesini önleyen kurallar.

Defter Colab ortamı için hazırlanmıştır. VS Code'da açılıp incelenebilir; yerel bilgisayarda doğrudan çalıştırılması ek kurulum ve uyarlama gerektirebilir.

## Bağlantılar

- [Google Colab defteri](https://colab.research.google.com/drive/1qj3FB3zO5_Y8rhPxbqb9qtfJqn8_t9XF?usp=sharing)
- [Model ve proje raporu](https://huggingface.co/sedaahi/Kivi-1.5B)
- [GGUF model dosyaları](https://huggingface.co/sedaahi/Kivi-1.5B-GGUF)
- [Eğitim verisi ve ölçümler](https://huggingface.co/datasets/sedaahi/kivi-1.5b-veri)
- [Web uygulaması kaynak dosyaları](https://huggingface.co/sedaahi/Kivi-1.5B-GGUF/tree/main/space)

Model ağırlıkları Hugging Face üzerinde tutulmaktadır. Web uygulaması kaynak dosyaları bağlantısı, yayındaki bir site adresi değildir.
