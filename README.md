# AI Wordle

**AI Wordle**, İngilizce [Wordle](https://www.nytimes.com/games/wordle/index.html) oyununu oynayan olasılık tabanlı bir yapay zeka ajanıdır. Ajan, harf frekans analizi kullanarak her turda en yüksek bilgi kazancını sağlayacak tahmini seçer.

## İçerik

| Dosya | Açıklama |
|---|---|
| `YAP441_PROJE.ipynb` | Wordle oynayan kural-tabanlı yapay zeka (ana proje) |
| `M1.ipynb` | Türkçe soru-cevap verisiyle ince ayar yapılan Llama-3-8B modeli |

## Nasıl Çalışır?

### YAP441_PROJE.ipynb — Wordle Yapay Zekası

`AI_Player` sınıfı iki aşamalı bir olasılık stratejisi uygular:

- **Başlangıç (kelime havuzu ≥ 900):** Tüm pozisyonlar üzerinden toplam harf frekansına bakılarak "temel olasılık puanı" hesaplanır; her harfi farklı olan, en sık geçen harfleri içeren kelimeler tercih edilir.
- **Daralan havuz (< 900 kelime):** Her pozisyon için ayrı ayrı frekans hesaplanır; böylece "karmaşık olasılık puanı" elde edilir ve bu puan pozisyon bilgisini de içerir.

Her tahminden sonra gelen geri bildirim (`G` = yeşil / doğru konum, `Y` = sarı / yanlış konum, `W` = gri / kelimede yok) kelime listesini filtreler ve olasılıklar yeniden hesaplanır.

`Game` sınıfı 6 hakkıyla oynanan bir oyunu yönetir ve gerçek Wordle kurallarını uygular.

### M1.ipynb — LLM İnce Ayarı

[Unsloth](https://github.com/unslothai/unsloth) kütüphanesi ile `unsloth/llama-3-8b-bnb-4bit` modeli, [boun-tabi/squad_tr](https://huggingface.co/datasets/boun-tabi/squad_tr) Türkçe soru-cevap veri seti üzerinde LoRA (rank=16) kullanılarak ince ayara tabi tutulmuştur.

## Veri

Wordle kelime listesi aşağıdaki kaynaktan alınmış ve CSV formatına dönüştürülmüştür:

> https://github.com/tabatkins/wordle-list/blob/main/words

## Gereksinimler

```
pandas
numpy
```

## Kullanım

1. Bu repoyu klonlayın:
   ```bash
   git clone https://github.com/ncunsoy/AIWordle.git
   cd AIWordle
   ```
2. Yukarıdaki veri bağlantısından `words.csv` dosyasını indirin ve proje klasörüne koyun.
3. `YAP441_PROJE.ipynb` dosyasını Jupyter ortamında açın.
4. **İlk hücre** `AI_Player` ve `Game` sınıflarını tanımlar.
5. **İkinci hücre** yapay zekaya tek bir oyun oynatır.
6. **Üçüncü hücre** 100 oyunluk bir simülasyon çalıştırır ve şu istatistikleri toplar:
   - `success` — kazanılan oyun sayısı
   - `word_dict` — kaybedilen oyunlardaki hedef kelimeler
   - `score_dict` — kaybedilen oyunlardaki son tur skorları
   - `vowel_dict` — kaybedilen oyunlardaki kelimelerin sesli harf dağılımı
   - `letter_dict` — kaybedilen oyunlardaki harf dağılımı

## Katkıda Bulunma

Çekme istekleri memnuniyetle karşılanır. Önemli değişiklikler için lütfen önce bir konu (issue) açarak ne değiştirmek istediğinizi tartışın.

## Lisans

[MIT](https://choosealicense.com/licenses/mit/)
