# 🧠 AI Ke Building Blocks: Tokens Aur Embeddings 🧱

*Samjho kaise AI hamari bhasha ko chote tukdon aur meaning numbers mein badalta hai*

---

Namaste dosto! 👋 Welcome back to our AI journey! Pichhle Chapter mein humne apne pehle AI dost, Phi-3, se baat ki thi aur usse joke generate karwaya tha. Mazaa aaya tha na? 😄

Lekin AI model asal mein hamari bhasha ko kaise samajhta hai? Woh "chicken" ya "joke" jaise shabdon ko computer ke liye useful cheez mein kaise badalta hai? Is Chapter mein hum yahi seekhenge!

Hum explore karenge Language Models ke do bahut important building blocks: **Tokens** aur **Embeddings**. Socho yeh AI ke woh chote chote parts hain jinse woh hamari baatein samajhta hai.

Yeh guide ke Chapter 2 ke practical ko samjhaati hai. Agar tum is topic mein aur bhi andar tak jaana chahte ho, toh woh book bahut help karegi!

---

Toh, apni kursi ki peti baandh lo, kyunki hum AI ke andar thoda aur gehrai se utarne wale hain! 🌊

---

## Table of Contents

*   [Intro: AI Ke Building Blocks](#-ai-ke-building-blocks-tokens-aur-embeddings-🧱)
*   [Setup Taiyaari: Magic Kit Jaisa (Optional Step)](#setup-taiyaari-magic-kit-jaisa-optional-step)
    *   [GPU Power (Super Engine!)](#gpu-power-super-engine)
    *   [Packages Install Karna (Tools Ikhatte Karna)](#packages-install-karna-tools-ikhatte-karna)
*   [Hamare AI Dost Ko Load Karna](#hamare-ai-dost-ko-load-karna)
    *   [Code: Model Aur Tokenizer Load Karna](#code-model-aur-tokenizer-load-karna)
    *   [Code: AI Se Text Generate Karna (Tokenization ka pehla roop)](#code-ai-se-text-generate-karna-tokenization-ka-pehla-roop)
    *   [Code: Input Tokens Ke IDs Dekhna](#code-input-tokens-ke-ids-dekhna)
    *   [Code: Har ID Ko Wapas Text Mein Badal Kar Dekhna](#code-har-id-ko-wapas-text-mein-badal-kar-dekhna)
    *   [Code: Full Output Ke IDs Dekhna](#code-full-output-ke-ids-dekhna)
    *   [Code: Kuch IDs Ko Decode Karke Samajhna](#code-kuch-ids-ko-decode-karke-samajhna)
*   [Alag Alag AI Tokenizers Ko Compare Karna](#alag-alag-ai-tokenizers-ko-compare-karna)
    *   [Code: Tokenizer Compare Karne Wala Function](#code-tokenizer-compare-karne-wala-function)
    *   [Code: Test Sentence Taiyaar Karna](#code-test-sentence-taiyaar-karna)
    *   [Code: BERT Tokenizer Se Dekhna (Uncased)](#code-bert-tokenizer-se-dekhna-uncased)
    *   [Code: BERT Cased Tokenizer Se Dekhna](#code-bert-cased-tokenizer-se-dekhna)
    *   [Code: GPT-2 Tokenizer Se Dekhna](#code-gpt-2-tokenizer-se-dekhna)
    *   [Code: Flan-T5 Tokenizer Se Dekhna](#code-flan-t5-tokenizer-se-dekhna)
    *   [Code: StarCoder2 Tokenizer Se Dekhna](#code-starcoder2-tokenizer-se-dekhna)
    *   [Code: Phi-3 Tokenizer Se Dekhna](#code-phi-3-tokenizer-se-dekhna)
*   [Contextualized Word Embeddings (Meaning Numbers Jo Badalte Hain)](#contextualized-word-embeddings-meaning-numbers-jo-badalte-hain)
    *   [Code: Embedding Model Load Karna Aur Embeddings Lena](#code-embedding-model-load-karna-aur-embeddings-lena)
    *   [Code: Embedding Ke Numbers Ka Shape Dekhna](#code-embedding-ke-numbers-ka-shape-dekhna)
    *   [Code: Embedding Model Ke Tokens Dekhna](#code-embedding-model-ke-tokens-dekhna)
    *   [Code: Raw Embedding Numbers Dekhna](#code-raw-embedding-numbers-dekhna)
*   [Text Embeddings (Poore Sentence Ya Document Ke Liye Meaning Numbers)](#text-embeddings-poore-sentence-ya-document-ke-liye-meaning-numbers)
    *   [Code: Sentence Embedding Model Load Karna Aur Embedding Lena](#code-sentence-embedding-model-load-karna-aur-embedding-lena)
    *   [Code: Sentence Embedding Ke Numbers Ka Shape Dekhna](#code-sentence-embedding-ke-numbers-ka-shape-dekhna)
*   [Word Embeddings Jo LLMs Se Purane Hain (Non-Contextual)](#word-embeddings-jo-llms-se-purane-hain-non-contextual)
    *   [Code: Purana Embedding Model (GloVe) Load Karna](#code-purana-embedding-model-glove-load-karna)
    *   [Code: GloVe Se Similar Words Dhundhna](#code-glove-se-similar-words-dhundhna)
*   [Embedding Se Song Recommend Karna (Ek Real-Life Example!)](#embedding-se-song-recommend-karna-ek-real-life-example)
    *   [Code: Song Playlist Data Load Karna](#code-song-playlist-data-load-karna)
    *   [Code: Sample Playlists Dekhna](#code-sample-playlists-dekhna)
    *   [Code: Playlists Par Naya Embedding Model (Word2Vec) Train Karna](#code-playlists-par-naya-embedding-model-word2vec-train-karna)
    *   [Code: Train Kiye Model Se Similar Song IDs Dhundhna](#code-train-kiye-model-se-similar-song-ids-dhundhna)
    *   [Code: Original Song Ke Details Dekhna](#code-original-song-ke-details-dekhna)
    *   [Code: Recommendations Dikhane Wala Function Banana](#code-recommendations-dikhane-wala-function-banana)
    *   [Code: Song 2172 Ke Liye Recommendations Dekhna](#code-song-2172-ke-liye-recommendations-dekhna)
    *   [Code: Song 842 Ke Liye Recommendations Dekhna](#code-song-842-ke-liye-recommendations-dekhna)
*   [Seekhe Hue Shabd (Glossary)](#seekhe-hue-shabd-glossary)
*   [Summary: Kya Seekha Aur Aage Kya?](#summary-kya-seekha-aur-aage-kya)

---

## Setup Taiyaari: Magic Kit Jaisa (Optional Step)

Agar tum yeh notebook Google Colab par chala rahe ho (jahan computers cloud mein hote hain, jaise tumhara Google Drive files online save karta hai!), toh tumhe kuch special "tools" (packages) install karne padenge. Yeh tools AI model aur embeddings ke saath kaam karne ke liye zaroori hain. Agar tumhare paas pehle se Python aur zaroori libraries install hain ek powerful computer par (GPU ke saath!), toh tum yeh steps skip kar sakte ho.

Is code block ke aage se `#` hata do aur isko run karo agar tum Colab mein ho aur pehli baar yeh packages install kar rahe ho.

---

💡 **NOTE**: Hum AI models aur embeddings ko tez chalaane ke liye **GPU** (Super Engine!) use karna chahte hain. Google Colab mein upar menu mein jao:
**Runtime > Change runtime type > Hardware accelerator > GPU > GPU type > T4**.\
Yeh step bahut important hai speed ke liye!

---

```python
# %%capture # Yeh command output ko chhupa deta hai, taaki screen zyada bhare nahi install hone ke waqt.
# !pip install transformers>=4.41.2 sentence-transformers>=3.0.1 gensim>=4.3.2 scikit-learn>=1.5.0 accelerate>=0.31.0 # Yeh main command hai tools install karne ke liye.

# ! ka matlab hai ki yeh command seedha computer ke andar chal rahi hai (jaise terminal mein).
# pip install matlab naye software packages download karke daal do.
# transformers: AI models ke liye tool (version 4.41.2 ya naya) - AI brain aur translator load karne ke liye.
# sentence-transformers: Poore sentence ke liye meaning numbers banane ka tool (version 3.0.1 ya naya).
# gensim: Purane tarike ke word embeddings (meaning numbers) aur playlist analysis ke liye tool (version 4.3.2 ya naya).\
# scikit-learn: Kuch extra math ke tools jo shayad internally use hon (version 1.5.0 ya naya).
# accelerate: AI ko tez chalane mein help karta hai (version 0.31.0 ya naya).

# Yeh sab tools hamare AI experiment ke liye zaroori hain. Jaise science kit ke tools ko box se nikalna.
```

**Yeh Code Kya Karta Hai? 🤔**

Agar tum Google Colab par ho, toh yeh code kuch special software "tools" (packages) install karta hai jo humein AI model aur embeddings ke saath kaam karne ke liye chahiye. Socho jaise kisi game ko khelne ke liye usko download karna padta hai, waise hi yeh tools AI ke liye download ho rahe hain. `transformers`, `sentence-transformers`, `gensim`, `scikit-learn`, aur `accelerate` naam ke yeh tools chapter ke alag alag sections mein use honge.

---

## Hamare AI Dost Ko Load Karna

Pichhle chapter ki tarah, sabse pehle hum apna AI dost (model) aur uska translator (tokenizer) load karenge. Is chapter mein hum unko alag alag rakhenge taaki hum dekh sakein ki tokenizer kaise kaam karta hai.

### Code: Model Aur Tokenizer Load Karna

Hum Microsoft ke Phi-3 model aur uske tokenizer ko load karenge, aur unhein GPU par daal denge taaki tez processing ho.

```python
# transformers library se model aur tokenizer load karne ke blueprints laate hain.
from transformers import AutoModelForCausalLM, AutoTokenizer

# Ab hamara AI dost (model) load karte hain.
# Yeh Microsoft ka Phi-3-mini-4k-instruct model hai.
# from_pretrained matlab pehle se train kiye hue model ko download aur load karo.
# device_map="cuda": Isko GPU par load karo, taaki tez chale (Super Engine!).
# torch_dtype="auto": Data types ko automatically optimize karo performance ke liye.
# trust_remote_code=False: Security ke liye ek setting.
model = AutoModelForCausalLM.from_pretrained(
    "microsoft/Phi-3-mini-4k-instruct",
    device_map="cuda",
    torch_dtype="auto",
    trust_remote_code=False,
)

# Ab AI dost ka translator (tokenizer) load karte hain.
# Iska naam bhi model ke naam jaisa hi hai taaki yeh sahi match ho.
tokenizer = AutoTokenizer.from_pretrained("microsoft/Phi-3-mini-4k-instruct")

# Yei! Hamara AI dost aur uska personal translator ab ready hain! 🎉
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code `transformers` library se hamara AI dost (model) aur uska translator (tokenizer) load karta hai. `AutoModelForCausalLM` AI model load karta hai (jo text generate kar sakta hai) aur `AutoTokenizer` uska corresponding tokenizer. Hum model ka naam (`"microsoft/Phi-3-mini-4k-instruct"`) bataate hain, aur `device_map="cuda"` use karke isko GPU par load karte hain taaki yeh tez kaam kare. Yeh steps zaroori hain taaki hamara AI dost taiyaar ho baat karne ke liye!

### Code: AI Se Text Generate Karna (Tokenization ka pehla roop)

Hum ek prompt denge aur AI se chota sa jawab generate karwayenge. Is process ke peeche hi tokenization kaam karti hai।

```python
# Yeh woh prompt hai jo hum AI model ko denge (hamara instruction).
# Hum email likhne ko bol rahe hain aur "<|assistant|>" se bata rahe hain ki ab AI ki baari hai jawab dene ki.
prompt = "Write an email apologizing to Sarah for the tragic gardening mishap. Explain how it happened.<|assistant|>"

# Ab hum is prompt ko AI samajhne wali language (numbers/tokens) mein badlenge using tokenizer.\
# tokenizer(prompt, return_tensors=\"pt\"): Prompt lo aur isko PyTorch tensor (computer friendly numbers) mein badal do.\
# .input_ids: Sirf woh numbers chahiye jo text ko represent karte hain.\
# .to(\"cuda\"): In numbers ko GPU par bhej do, taaki AI unko tez process kar sake.\
input_ids = tokenizer(prompt, return_tensors="pt").input_ids.to("cuda")

# Ab hum AI model ko yeh numbers (input_ids) denge aur usse text generate karwayenge.\
# model.generate(): Model ko bolo naya text banao.\
# input_ids=input_ids: Yeh numbers hamare sawal/instruction hain.\
# max_new_tokens=20: Zyada se zyada 20 naye tokens (words/pieces) banao (taaki bahut lamba jawab na aaye).\
generation_output = model.generate(
  input_ids=input_ids,
  max_new_tokens=20
)

# Ab jo naye numbers bane hain (generation_output), unko wapas hamari bhasha (text) mein badlenge.\
# tokenizer.decode(): Numbers lo aur unko text mein badal do.\
# generation_output[0]: generation_output ek list mein hota hai, uska pehla item lo (hamara jawab).\
# print(): Text ko screen par dikha do!\
print(tokenizer.decode(generation_output[0]))

# Output mein dekho, AI ne email ka Subject aur \"Dear\" likhna shuru kar diya hai! Yeh generated text hai.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code dikhata hai ki kaise hum ek prompt taiyaar karte hain aur phir usko `tokenizer` use karke numbers (`input_ids`) mein badalte hain. Yeh pehla step hai **Tokenization** ka! Phir AI `model.generate()` function use karke un numbers se naye numbers banata hai (naya text sochta hai). Aur finally, `tokenizer.decode()` se un naye numbers ko wapas hamari samajh mein aane wali bhasha (text) mein badal dete hain. Yeh Language Models ke kaam karne ka core idea hai - text ko numbers, numbers ko naye numbers, aur naye numbers ko wapas text mein badalna!

### Code: Input Tokens Ke IDs Dekhna

Chalo dekhte hain ki hamara original prompt "Write an email apologizing..." numbers mein kaisa dikhta hai. Har number ek token ko represent karta hai।

```python
# Humne jo prompt ko numbers mein badla tha (input_ids), ab usko dekhte hain.\
# input_ids ek tensor hai, usko print karne se uske numbers dikhte hain.\
# Har number ek token ka ID hai.\
print(input_ids)

# Output mein woh lambi list computer ke numbers hain! Yeh AI ki bhasha hai.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code dikhata hai ki hamare prompt (`input_ids`) ko tokenizer ne kin numbers mein badla hai. Computer ke liye hamari bhasha numbers mein store hoti hai. Har number ek **Token ID** hai, jo ek specific token (chota text ka tukda) ko represent karta hai।

### Code: Har ID Ko Wapas Text Mein Badal Kar Dekhna

Ab dekhte hain ki woh numbers wapas text mein kaise badalte hain, ek ek token karke! Isse pata chalega ki tokenizer ne hamare sentence ko kin exact tukdon (tokens) mein toda hai।

```python
# Ab hum wohi numbers (input_ids) lenge aur dekhenge ki har number kis text ke tukde ko represent karta hai.\
# for id in input_ids[0]: input_ids list ke pehle item (hamara sentence) mein har number (id) par jao ek-ek karke.\
# print(tokenizer.decode(id)): Har number (id) ko wapas text mein badlo (decode karo) aur screen par dikhao.\
# Har token alag line mein print hoga.\
for id in input_ids[0]:
   print(tokenizer.decode(id))

# Output mein dekho, hamara original sentence kaise chote chote tokens mein toot gaya hai!\
# Kuch tokens poore words hain (\"Write\", \"an\"), aur kuch words tukdon mein hain (\"apolog\", \"izing\").\
# Special tokens bhi hain jaise \"<s>\" (sentence start) aur \"<|assistant|>\" (AI ki baari ka token).\
# Yeh hai tokenizer ka kaam!
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code dikhata hai ki hamare prompt ke numbers (Token IDs) ko agar wapas text mein badlein ek ek karke, toh kya banta hai. Yeh woh **Tokens** hain jinmein tokenizer ne hamare original text ko toda tha. Kuch tokens poore shabd hote hain, aur kuch shabdon ke tukde, punctuation, ya special symbols hote hain. Yeh dikhata hai ki AI hamari bhasha ko itne fine-grained level par process karta hai।

### Code: Full Output Ke IDs Dekhna

Jab AI jawab generate karta hai, toh woh bhi numbers mein hi hota hai. Chalo uske numbers dekhte hain।

```python
# Ab dekhte hain ki AI ne jo naya text generate kiya (generation_output), woh numbers mein kaisa dikhta hai.\
# Ismein hamare input numbers bhi shamil hote hain shuru mein, aur phir AI ke banaye naye numbers.\
# output variable ko print karne se uska content (numbers) dikhta hai.\
generation_output

# Output mein dekho, shuru ke numbers hamare input numbers jaise hain, aur unke baad kuch naye numbers aa gaye hain.\
# Yeh naye numbers hi AI ka generated jawab hai numbers mein!
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code `generation_output` variable ko dikhata hai, jismein AI model ka poora output store hai, numbers (Token IDs) ke roop mein. Is list/tensor mein shuru ke IDs wohi hain jo input mein the, aur baad ke IDs woh hain jo model ne generate kiye hain (jo text humne generate karke dekha tha, jaise "Subject: My Sincere Apologies for the Gardening Mishap\n\nDear").

### Code: Kuch IDs Ko Decode Karke Samajhna

AI ne jo numbers generate kiye hain, unmein se kuch IDs ko decode karke dekhte hain ki unka kya matlab hai। Humne pichle output mein kuch interesting IDs dekhe the।

```python
# Tokenizer mein kuch specific IDs ko dekhte hain ki woh kya text banate hain.\
# Hum woh IDs pick kar rahe hain jo hamein pichhle generation_output mein dikhe the.\
# Dekhte hain ID 3323 kya hai? (Yeh ek ID hai jo humne output numbers mein dekha tha)\
print(tokenizer.decode(3323))\
# Dekhte hain ID 622 kya hai? (Yeh bhi output numbers mein tha)\
print(tokenizer.decode(622))\
# Ab dono ko saath mein decode karte hain (list mein daal kar). Dekhte hain kya pura word banta hai?\
# List of IDs dene se tokenizer unko jod kar text banata hai.\
print(tokenizer.decode([3323, 622]))\
# Ek aur ID dekhte hain, 29901. (Yeh bhi output numbers mein tha)\
print(tokenizer.decode(29901))\

# Output mein dekho, \"Subject\" do alag alag IDs se bana hai (\"Sub\" aur \"ject\"). Yeh dikhata hai ki words tukdon mein bhi toot sakte hain.\
# Colon (\":\") ka bhi ek alag ID hai.\
# Yeh dikhata hai ki tokenizer words ko kaise tukdon mein todta hai (tokenization).
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code kuch specific Token IDs ko lekar `tokenizer.decode()` function use karke unka text dikhata hai. Isse hum dekh sakte hain ki kaise kuch words (`Subject`) ek se zyada tokens mein divide hote hain aur kaise punctuation marks (:) bhi alag tokens ho sakte hain. Yeh hai **Tokenization** process! Alag alag tokenizers words ko alag alag tarike se break karte hain, jaisa hum aage dekhenge।

---

## Alag Alag AI Tokenizers Ko Compare Karna

Jaise har insaan thodi alag bhasha bolta aur samajhta hai, waise hi alag alag AI models ke **Tokenizers** bhi thode alag ho sakte hain. Ek tokenizer text ko ek tarike se tod sakta hai, aur doosra thoda alag tarike se. Yeh ispar depend karta hai ki model ko kaise train kiya gaya hai aur kaunsi **Tokenization strategy** use ki gayi hai (jaise WordPiece, BPE, SentencePiece)।

Chalo dekhte hain ki ek hi sentence ko alag alag popular AI models ke tokenizers kaise break karte hain. Hum ek chota sa helper function banayenge isko aasan banane ke liye.

### Code: Tokenizer Compare Karne Wala Function

Yeh function hamare liye kisi bhi sentence ko kisi bhi tokenizer se tokens mein tod kar colorful tarike se dikhayega।

```python
# Zaroori tools laate hain transformers library se - model nahi, sirf tokenizer!\
from transformers import AutoTokenizer

# Kuch colors define karte hain, taaki jab hum tokens dekhein toh woh colorful dikhein! ✨
# Yeh sirf dikhane ke liye hai, code ke asal logic ke liye zaroori nahi.\
colors_list = [
    '102;194;165', # Color 1 (Greenish)
    '252;141;98',  # Color 2 (Orangish)
    '141;160;203', # Color 3 (Blueish)
    '231;138;195', # Color 4 (Pinkish)
    '166;216;84',  # Color 5 (Light Green)
    '255;217;47'   # Color 6 (Yellowish)
]

# Yeh ek function hai jo humein dikhayega ki koi sentence tokens mein kaise toot ta hai.\
# Input mein sentence aur tokenizer ka naam lega.\
def show_tokens(sentence, tokenizer_name):\
    print(f"\\n--- Tokenizer: {tokenizer_name} ---") # Tokenizer ka naam print karo taaki pata chale kaunsa use kar rahe hain.\
    # Us naam ka tokenizer load karte hain.\
    # AutoTokenizer automatically sahi type ka tokenizer dhundh leta hai naam se.\
    tokenizer = AutoTokenizer.from_pretrained(tokenizer_name)
    # Sentence ko tokens (numbers) mein badalte hain.\
    # .input_ids se numbers ki list milti hai.\
    token_ids = tokenizer(sentence).input_ids
    # Har token ID par jao list mein ek-ek karke.\
    # enumerate se humein ID aur uska index (position) dono milte hain.\
    for idx, t in enumerate(token_ids):
        # Ab har token ko ek unique color mein print karte hain.\
        # Color change karne ke liye special ANSI escape codes use hote hain (\\x1b[...m).\
        # colors_list[idx % len(colors_list)] yeh ensure karta hai ki colors repeat hon agar tokens zyada hon.\
        # tokenizer.decode(t) actual token text nikalta hai us number (ID) se.\
        # end=' ' matlab print karne ke baad new line nahi, balki ek space do.\
        print(\
            f'\\x1b[0;30;48;2;{colors_list[idx % len(colors_list)]}m' + # Color start code (defines background color)\
            tokenizer.decode(t) + # Actual token text\
            '\\x1b[0m', # Color end code (resets text formatting to normal)\
            end=' ' # Print ke baad space do
        )
    # Jab saare tokens print ho jaayein, ek naya line shuru karte hain taaki agla output saaf dikhe.\
    print()
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code ek helper function `show_tokens` banata hai. Is function ka kaam hai ki tum usko koi sentence aur kisi bhi AI model ke tokenizer ka naam do, aur woh tumhe dikhayega ki woh particular tokenizer us sentence ko kaise chote chote **Tokens** mein todta hai. Ismein colors ka use kiya gaya hai taaki har token alag alag dikhe, samajhna aasan ho jaye! Yeh function chapter ke alag alag tokenizers ko compare karne mein bahut help karega.

### Code: Test Sentence Taiyaar Karna

Hum ek sentence banayenge jismein alag alag tarah ki cheezein hain, taaki hum dekh sakein ki tokenizers unhe kaise handle karte hain।

```python
# Yeh hamara test sentence hai jisko hum alag alag tokenizers se check karenge.\
# Ismein alag alag tarah ki cheezein hain:\
# - Normal English words\
# - CAPITALIZATION (Bade akshar)\
# - Emojis (🎵)\
# - Non-English characters (鸟 - Chinese word for bird)\
# - Programming keywords (False, None, elif, ==, >=, else:)\
# - Spaces, including multiple spaces and tabs (\"    \", \"       \")\
# - Numbers and math operators (12.0*50=600)\

text = \"\"\"\
English and CAPITALIZATION\
🎵 鸟\
show_tokens False None elif == >= else: two tabs:\"    \" Three tabs: \"       \"\
12.0*50=600\
\"\"\"
# Yeh test sentence dikhayega ki kaise different tokenizers alag alag types ke text ko handle karte hain.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code ek multi-line string variable `text` banata hai. Is string mein humne jaan boojh kar alag alag tarah ke characters, words (capital letters mein bhi), symbols (emoji aur Chinese character), numbers, operators, aur spaces (tabs) dale hain. Hum is sentence ko use karke dekhenge ki alag alag tokenizers in sab cheezon ko kaise tokens mein todte hain. Har tokenizer ka apna tarika hota hai!

### Code: BERT Tokenizer Se Dekhna (Uncased)

Chalo, ab `show_tokens` function use karke dekhte hain ki Google ke **BERT** model ka \"uncased\" tokenizer is sentence ko kaise tokens mein todta hai. \"Uncased\" matlab yeh bade aksharon ko chote aksharon mein badal deta hai।

```python
# show_tokens function ko hamara test text aur BERT uncased tokenizer ka naam do.\
# \"bert-base-uncased\" Hugging Face models mein ek standard naam hai.\
# \"uncased\" matlab yeh input ke bade letters ko chote mein convert kar deta hai.\
show_tokens(text, "bert-base-uncased")

# Output dekho! Har rang ek alag token hai.\
# Notice karo \"English\" aur \"CAPITALIZATION\" chote letters mein aa gaye hain.\
# \"CAPITALIZATION\" jaisa lamba word tukdon mein toot gaya hai (##ization).\
# ## ka matlab hai ki yeh token pichhle token ka continuation hai.\
# Emojis aur Chinese characters ke liye \"[UNK]\" tokens aa rahe hain (Unknown tokens).\
# Special tokens jaise [CLS] (Classify) aur [SEP] (Separator) bhi dikh rahe hain BERT ke liye.\
# Tabs ke liye \"/t\" aa raha hai.\
# Yeh is tokenizer ka tarika hai text ko numbers mein badalne ka.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code hamare test `text` ko Google ke BERT model ke "uncased" tokenizer se process karke dikhata hai. "Uncased" ka matlab hai ki yeh tokenizer bade letters (CAPITALIZATION) ko chote letters mein badal deta hai. Output mein dekho, "English" aur "CAPITALIZATION" chote letters mein aa rahe hain. Saath hi, kuch tokens ke aage `##` laga hai, iska matlab woh kisi bade shabd ka hissa hain. Aur jo symbols aur Chinese character hain, unko yeh `[UNK]` (Unknown) token bana deta hai, kyunki yeh tokenizer unhe pehchanta nahi. Tabs (`    `) ko yeh `\\t` (tab character) mein badal deta hai. Yeh tokenizer sentence ke shuru aur end mein special tokens `[CLS]` aur `[SEP]` bhi add karta hai.

### Code: BERT Cased Tokenizer Se Dekhna

Ab Google ke BERT model ka \"cased\" tokenizer dekhte hain. \"Cased\" matlab yeh bade aksharon ko vaise hi rakhta hai, badalta nahi।"

```python
# show_tokens function ko hamara test text aur BERT cased tokenizer ka naam do.\
# \"bert-base-cased\" wala version input ke capital letters ko maintain rakhta hai.\
show_tokens(text, "bert-base-cased")

# Output dekho! Ab \"English\" aur \"CAPITALIZATION\" mein bade letters vaise hi hain.\
# \"CAPITALIZATION\" ab aur bhi zyada tukdon mein toot gaya hai (CA, ##PI, ##TA, ##L, ##I, ##Z, ##AT, ##ION).\
# Baki chizein uncased jaisi hi hain - [UNK] for unknown chars, /t for tab, [CLS], [SEP].\
# Capital letters ko maintain rakhne se tokens thode alag ho gaye.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code hamare test `text` ko Google ke BERT model ke "cased" tokenizer se process karke dikhata hai. "Cased" ka matlab hai ki yeh tokenizer bade letters (CAPITALIZATION) ko alag tarike se treat karta hai, unhe chote letters mein *nahi* badalta. Output mein dekho, "English" aur "CAPITALIZATION" ab tukdon mein hain aur unke capital letters preserve hue hain. Yeh tokenizer bhi `##` use karta hai aur special characters/emojis ke liye `[UNK]` dikhata hai. Tabs (`    `) ko yeh `\\t` (tab character) mein badal deta hai. Yeh tokenizer bhi `[CLS]` aur `[SEP]` tokens add karta hai.

### Code: GPT-2 Tokenizer Se Dekhna

Ab OpenAI ke **GPT-2** model ka tokenizer dekhte hain. Yeh thoda alag tarika use karta hai (BPE - Byte Pair Encoding) aur spaces ko bhi tokens mein shamil karta hai।

```python
# show_tokens function ko hamara test text aur GPT-2 tokenizer ka naam do.\
# \"gpt2\" OpenAI ka popular model hai.\
# Iska tokenizer Byte Pair Encoding (BPE) use karta hai aur spaces ko word ka part treat karta hai.\
show_tokens(text, "gpt2")

# Output dekho! Yeh tokenizer word ke aage space ko bhi ek token bana deta hai (bahut se tokens space symbol se shuru ho rahe hain).
# Capitalization ko yeh maintain rakhta hai, jaise BERT cased.\
# Special characters/emojis ke liye yahan ek alag hi symbol � aa raha hai (Unicode replacement character).\
# Tabs bhi multiple space tokens mein toot rahe hain.\
# Har tokenizer ka apna signature style hai! GPT-2 ka space handling BERT se alag hai.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code hamare test `text` ko OpenAI ke GPT-2 model ke tokenizer se process karke dikhata hai. GPT-2 ka tokenizer thoda alag hai. Yeh words ke aage space ko bhi ek alag token bana deta hai (output mein dekho, bahut saare tokens space se shuru ho rahe hain). Yeh bhi words ko tukdon mein todta hai par alag tarike se, aur special characters/emojis ke liye `�` jaisa token dikhata hai. Tabs (`    `) ko bhi spaces ke tokens mein tod deta hai. Is tokenizer mein BERT jaise `[CLS]` ya `[SEP]` tokens nahi hote.

### Code: Flan-T5 Tokenizer Se Dekhna

Google ke ek aur model, **Flan-T5**, ka tokenizer dekhte hain।

```python
# show_tokens function ko hamara text aur Flan-T5 tokenizer ka naam do.\
# \"google/flan-t5-small\" Google ka ek encoder-decoder model hai.\
# Iska tokenizer SentencePiece use karta hai.\
show_tokens(text, "google/flan-t5-small")

# Output dekho! Yeh tokenizer bhi GPT-2 jaisa hai, spaces ko word ka part treat karta hai.\
# Special characters/emojis ke liye yahan bhi � symbol aa raha hai.\
# Tabs bhi multiple space tokens mein toot rahe hain.\
# Ismein SentencePiece ka alag tarika dikh raha hai tokenization ka. Start aur end mein </s> tokens bhi hain.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code hamare test `text` ko Google ke Flan-T5 model ke tokenizer se process karke dikhata hai. Flan-T5 tokenizer GPT-2 jaisa hai ki yeh space ko word ka part treat karta hai. Yeh special characters/emojis ke liye `�` dikhata hai aur tabs ko multiple space tokens mein todta hai. Ismein SentencePiece tokenization use hoti hai, jo thodi alag hai, aur yeh sentence ke end mein `</s>` token add karta hai.

### Code: StarCoder2 Tokenizer Se Dekhna

BigCode ka **StarCoder2** model, jo code ke liye train hua hai, uska tokenizer dekhte hain। Yeh code ko kaise handle karta hai, yeh dekhna interesting hoga।

```python
# show_tokens function ko hamara text aur StarCoder2 tokenizer ka naam do.\
# \"bigcode/starcoder2-15b\" code-focused model hai.\
# Iska tokenizer bhi alag tarika use karta hai.\
# Note: Kuch bade models ke liye access request karna pad sakta hai Hugging Face par.\
show_tokens(text, "bigcode/starcoder2-15b")

# Output dekho! Is tokenizer ka tarika code friendly lagta hai.\
# Programming keywords aur symbols ko kaise handle karta hai yeh dhyan se dekho.\
# CAPITALIZATION ko maintain rakhta hai.\
# Emojis aur Chinese characters ke liye yahan bhi � hai.\
# Tabs ko yeh bhi space tokens mein tod raha hai.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code hamare test `text` ko BigCode ke StarCoder2 model ke tokenizer se process karta hai. Kyunki yeh model code par train hua hai, iska tokenizer programming related text ko alag tarike se treat kar sakta hai. Output mein dekho kaise yeh programming keywords (`False`, `None`, `elif`, `else`) aur operators (`==`, `>=`) ko tokens mein todta hai. Ismein bhi capital letters maintain rahte hain, emojis/special chars ke liye `�` hai, aur tabs spaces mein badal rahe hain.

### Code: Phi-3 Tokenizer Se Dekhna

Ab wapas hamare pehle chapter wale dost, **Phi-3**, ka tokenizer dekhte hain। Humne isko pehle bhi dekha tha, par ab isko doosre tokenizers se compare karte hain।

```python
# show_tokens function ko hamara text aur Phi-3 tokenizer ka naam do.\
# \"microsoft/Phi-3-mini-4k-instruct\" hamara main model hai.\
# Iska tokenizer bhi SentencePiece jaisa hai.\
show_tokens(text, "microsoft/Phi-3-mini-4k-instruct")

# Output dekho! Phi-3 ka tokenizer bhi spaces ko word ka part bana raha hai (GPT-2, Flan-T5 jaisa).\
# CAPITALIZATION ko maintain rakhta hai.\
# Emojis aur Chinese characters ke liye yahan bhi � symbol aa raha hai.\
# Tabs bhi spaces mein toot rahe hain.\
# Shuru mein koi special token nahi hai par end mein new line token aa raha hai.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code hamare test `text` ko Microsoft ke Phi-3 model ke tokenizer se process karta hai. Iska tokenizer SentencePiece jaise tarike use karta hai. Output mein dekho ki yeh bhi spaces ko word ka part bana deta hai (jaise GPT-2 aur Flan-T5). Capital letters maintain rahte hain, emojis/special characters ke liye `�` hai, aur tabs multiple space tokens mein badalte hain. Iska behavior dusre modern tokenizers se milta julta hai, lekin har ek mein thode variations hote hain.

---

## Contextualized Word Embeddings (Meaning Numbers Jo Badalte Hain)

Humne dekha ki text ko tokens mein kaise todte hain. Ab dekhte hain ki in tokens ko computer kaise samajhta hai. Computer in tokens ko **numbers** mein badalta hai. In numbers ko **Embeddings** kehte hain।

Modern Language Models (jaise BERT, GPT, Phi) mein, har token ko ek list of numbers se represent kiya jaata hai. Yeh numbers token ke "matlab" ko represent karte hain, par sabse khaas baat yeh hai ki yeh numbers **Contextualized** hote hain।

💡 **Analogy:** Socho, agar \"bank\" shabd sentence mein hai. \"River bank\" mein \"bank\" ka matlab alag hai \"money bank\" se. Ek normal dictionary mein \"bank\" ke do alag entries hongi. Par AI ke Contextualized Embeddings mein, \"river bank\" wala \"bank\" aur \"money bank\" wala \"bank\" ka **meaning number list alag alag** hoga! Yeh numbers us shabd ke aas paas ke shabdon par depend karte hain।

Hum ek BERT jaisa model (Microsoft ka DeBERTa) load karenge aur dekhenge ki yeh tokens ko kaise numbers mein badalta hai।

### Code: Embedding Model Load Karna Aur Embeddings Lena

Hum DeBERTa tokenizer aur model load karenge aur ek simple sentence ko process karke uske embeddings nikalenge।

```python
# Embeddings ke liye special models hote hain. Hum DeBERTa use karenge jo BERT jaisa hai.\
# transformers library se AutoModel aur AutoTokenizer laate hain.\
# AutoModel ek general AI model hai jo embeddings de sakta hai.\
from transformers import AutoModel, AutoTokenizer

# Ab ek tokenizer load karte hain jo DeBERTa ke liye bana hai.\
# \"microsoft/deberta-base\" ek standard DeBERTa model ka naam hai.\
tokenizer = AutoTokenizer.from_pretrained("microsoft/deberta-base")

# Ab Language Model load karte hain jo embeddings banayega.\
# Hum thoda chota version use kar rahe hain \"microsoft/deberta-v3-xsmall\" (tez chalega).\
# from_pretrained se model download aur load karo.\
# device_map=\"cuda\" se GPU par load karo.\
model = AutoModel.from_pretrained("microsoft/deberta-v3-xsmall")

# Ab ek simple sentence lete hain.\
sentence = 'Hello world'

# Sentence ko tokenizer se numbers (tokens) mein badalte hain.\
# return_tensors='pt' matlab PyTorch tensor format mein do.\
tokens = tokenizer(sentence, return_tensors='pt')\
# .to(\"cuda\") se numbers ko GPU par bhej do.\
tokens = {k: v.to(\"cuda\") for k, v in tokens.items()} # dictionary ke har item ko cuda par move karo.

# Ab in numbers (tokens) ko model ke andar se process karwate hain.\
# model(**tokens) matlab model ko tokens de kar uska output lo.\
# [0] se pehla output (embeddings) lete hain.\
output = model(**tokens)[0]

# Ab output variable mein hamare sentence ke embeddings store hain!
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code `transformers` library se ek tokenizer aur ek DeBERTa naam ka Language Model load karta hai. DeBERTa BERT jaisa hi ek model hai jo text ko samajh kar har token ke liye **Contextualized Embeddings** (meaning numbers) banata hai. Hum ek sentence ("Hello world") ko `tokenizer` use karke numbers mein badalte hain, aur phir un numbers ko `model` mein daal kar usse **embeddings** nikalte hain. `output` variable mein yahi embeddings store hote hain।

### Code: Embedding Ke Numbers Ka Shape Dekhna

Embeddings sirf ek number nahi hota, balki numbers ki puri list hoti hai (ek vector). Iski lambai ko **embedding size** kehte hain. Dekhte hain hamare `output` ka shape kya hai।

```python
# Hamare output (embeddings) ka shape (dimensions) dekhte hain.\
# .shape property se tensor ka shape pata chalta hai.\
output.shape

# Output mein dikhega \"torch.Size([1, 4, 384])\" (numbers thode alag ho sakte hain).\
# Iska matlab hai:\
# 1: Humne 1 sentence diya (Batch size).\
# 4: Hamare sentence mein 4 tokens the (\"[CLS]\", \"Hello\", \" world\", \"[SEP]\").\
# 384: Har token ke liye 384 numbers ki list mili hai (Embedding size).
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code hamare `output` embeddings variable ka `shape` print karta hai. Shape dikhata hai ki embeddings kaise organize hain. `torch.Size([1, 4, 384])` (numbers vary ho sakte hain) ka matlab hai: 1 sentence hai, usmein 4 tokens hain, aur har token 384 numbers ki list (vector) se represent ho raha hai. Yeh 384 **Embedding Size** hai।

### Code: Embedding Model Ke Tokens Dekhna

Jis sentence ka humne embedding nikala hai, uske tokens dekhte hain।

```python
# Jis sentence ke liye embeddings nikale hain ('Hello world'), uske tokens dekhte hain.\
# tokens['input_ids'][0] mein woh numbers hain.\
# for loop se har number (token ID) ko decode karke print karte hain.\
for token in tokens['input_ids'][0]:
    print(tokenizer.decode(token))

# Output mein dekho: [CLS], Hello, world, [SEP].\
# DeBERTa tokenizer ne \" Hello world\" ko teen tokens mein toda hai aur special tokens add kiye hain.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code dikhata hai ki DeBERTa tokenizer ne "Hello world" sentence ko kin tokens mein toda tha. Output mein `[CLS]`, `Hello`, ` world`, aur `[SEP]` dikhenge. `[CLS]` sentence start, `[SEP]` sentence end, aur ` Hello` mein shuru ka space dekho।

### Code: Raw Embedding Numbers Dekhna

Ab embeddings ke actual numbers dekhte hain। Yeh woh numbers hain jo AI model ne har token ke liye banaye hain।

```python
# Hamare output (embeddings) ke actual numbers dekhte hain.\
# output variable ko print karne se uske andar ke numbers dikh jaate hain.\
output

# Output mein bahut saare decimal numbers ki list dikhegi.\
# Yeh woh 384 numbers hain har token ke liye.\
# Yahi numbers AI model use karta hai aage ki processing ke liye aur meaning capture karte hain.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code `output` variable ka content print karta hai, jo ki hamare tokens ke liye bane hue **Contextualized Embeddings** ka tensor hai. Output mein bahut saare decimal numbers ki list dikhegi. Yeh har token ke "meaning" ka numerical representation hai, jo uske context ke hisaab se bana hai। Yahi numbers AI ke andar math karne aur baatein samajhne ke liye use hote hain।

---

## Text Embeddings (Poore Sentence Ya Document Ke Liye Meaning Numbers)

Kabhi kabhi humein Language Models se har token ka alag meaning number nahi chahiye hota, balki poore sentence ya poore document ka ek hi meaning number chahiye hota hai। Iske liye **Text Embeddings** ya **Sentence Embeddings** use hote hain।

💡 **Analogy:** Socho, tumhare paas ek paragraph hai kahani ka. Agar tum Text Embedding model use karoge, toh woh poore paragraph ko padh kar uske main idea ya theme ko ek hi list of numbers mein badal dega. Jaise paragraph ki summary ka number roop।

Hum `sentence-transformers` library use karenge jo aise models load karna aur use karna aasan banata hai।

### Code: Sentence Embedding Model Load Karna Aur Embedding Lena

Hum ek Sentence-BERT model load karenge aur ek sentence ka text embedding nikalenge।

```python
# sentence-transformers library se SentenceTransformer tool laate hain.\
from sentence_transformers import SentenceTransformer

# Ab ek Sentence Embedding model load karte hain.\
# \"sentence-transformers/all-mpnet-base-v2\" ek popular model hai jo sentence embeddings banane ke liye train hua hai.\
model = SentenceTransformer('sentence-transformers/all-mpnet-base-v2')

# Ab ek sentence lete hain jiska embedding nikalna hai.\
sentence = \"Best movie ever!\"

# Sentence ko model ke .encode() method se seedha text embedding (number list) mein badalte hain.\
# Yeh model poore sentence ko read karke ek single vector bana deta hai.\
vector = model.encode(sentence)

# Ab vector variable mein hamare sentence ka text embedding store hai.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code `sentence-transformers` library use karke ek Sentence-BERT model load karta hai. Yeh model specially design kiya gaya hai **Text Embeddings** ya **Sentence Embeddings** banane ke liye. Hum ek sentence (`"Best movie ever!"`) ko `model.encode()` function mein daal kar uska ek single numerical vector (`vector`) nikalte hain. Yeh vector poore sentence ke matlab ko represent karta hai।

### Code: Sentence Embedding Ke Numbers Ka Shape Dekhna

Dekhte hain ki Text Embedding ka shape kaisa hota hai. Humein ek hi vector milna chahiye poore sentence ke liye।

```python
# Hamare sentence embedding (vector) ka shape dekhte hain.\
# .shape property se is number list ki lambai pata chalegi.\
vector.shape

# Output mein dikhega \"(768,)\" (number alag ho sakta hai).\
# Iska matlab hai ki hamara sentence ek single list of 768 numbers se represent ho raha hai.\
# Yahan koi alag token ki dimension nahi hai, jaise contextualized embeddings mein thi. Yeh poore sentence ka ek vector hai.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code hamare `vector` variable ka `shape` print karta hai. Output `(768,)` (number vary ho sakta hai) dikhayega. Iska matlab hai ki hamara poora sentence ek single list of 768 numbers se represent ho raha hai. Contextualized embeddings se alag, yahan har token ka alag vector nahi hai, balki poore sentence ka ek consolidated vector hai। Yahi hain **Text Embeddings**।

---

## Word Embeddings Jo LLMs Se Purane Hain (Non-Contextual)

AI ki duniya mein Language Models (LLMs) naye hain. LLMs se pehle bhi words ko numbers mein badalne ke tarike the. Unhein **Word Embeddings** kehte the (jaise Word2Vec, GloVe)।

In purane embeddings mein ek shabd ka meaning number hamesha **same** rehta tha, bhale hi woh kisi bhi sentence mein aaye.

💡 **Analogy:** Wapas \"bank\" example par aao. Purane Word Embeddings mein, \"river bank\" wala \"bank\" aur \"money bank\" wala \"bank\" ka **meaning number list same** hoga. Jaise ek purani dictionary jismein \"bank\" ke alag entries hain par tumhein sentence padh kar samajhna padega ki kaunsa matlab use ho raha hai।

Inhein **Non-Contextual** embeddings kehte hain kyunki yeh context (aas paas ke shabd) par depend nahi karte।

Hum `gensim` library use karenge jo aise purane embeddings ke saath kaam karne mein help karta hai। Hum GloVe naam ka ek popular non-contextual embedding model load karenge।

### Code: Purana Embedding Model (GloVe) Load Karna

Hum `gensim.downloader` se ek pre-trained (pehle se train kiya hua) GloVe model download karke load karenge।

```python
# gensim library se downloader tool laate hain.\
import gensim.downloader as api

# Ab ek pre-trained embedding model download karke load karte hain.\
# api.load() se hum gensim ke data store se model download kar sakte hain.\
# \"glove-wiki-gigaword-50\": Yeh model ka naam hai - GloVe, Wikipedia par train hua, har word ke liye 50 numbers (vector size: 50).\
# Yeh file download hone mein thoda time lag sakta hai (approx 66MB).\
model = api.load("glove-wiki-gigaword-50")

# Ab hamara GloVe embedding model load ho gaya hai!
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code `gensim` library use karke एक **Non-Contextual Word Embedding** model download aur load karta hai jiska naam **GloVe** hai. Yeh model Wikipedia ke data par train hua hai aur har word ko 50 numbers ki list (vector) se represent karta hai। Yeh embeddings LLMs ke contextualized embeddings se alag hain kyunki ek word ka vector uske sentence par depend nahi karta।

### Code: GloVe Se Similar Words Dhundhna

In embeddings ka ek cool feature hai ki jin shabdon ka matlab similar hota hai, unke meaning numbers bhi ek doosre ke **paas** hote hain multi-dimensional space mein। Isliye hum `most_similar` function use karke kisi word ke sabse similar words dhundh sakte hain meaning ke hisaab se!

```python
# Ab load kiye hue GloVe model se \"king\" word ke sabse similar words dhundhte hain.\
# model['king']: \"king\" word ka 50 numbers wala vector nikalte hain.\
# model.most_similar(): Model ko ek vector do aur woh uske sabse paas wale word vectors dhundh kar unke words bata dega.\
# positive=[model['king']]: \"king\" ke vector ke similar words chahiye.\
# topn=11: Sabse similar 11 words batao (king ko chhod kar 10 chahiye, isliye 11 mang rahe hain).\
model.most_similar([model['king']], topn=11)

# Output mein dekho! \"king\" ke sabse similar words \"prince\", \"queen\", \"emperor\" jaise aa rahe hain.\
# Yeh dikhata hai ki in numbers ne shabdon ke matlab ko kitne acchi tarah se capture kiya hai.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code GloVe model ke `most_similar` function ka use karke "king" word ke embedding vector ke sabse paas (meaning mein similar) words dhundhta hai. Output mein aise words aate hain jo meaning ke hisaab se "king" se close hain (jaise "prince", "queen", "emperor"). Yeh dikhata hai ki kaise embeddings shabdik rishton (semantic relationships) ko numerical space mein capture kar sakte hain।

---

## Embedding Se Song Recommend Karna (Ek Real-Life Example!)

Embeddings ka ek real-life use case dekhte hain - gaane recommend karna! Jaise words similar hote hain meaning mein, waise hi hum gaano (songs) ko bhi numbers mein badal sakte hain aur phir similar gaane dhundh sakte hain। Yeh kaise karte hain? Hum dekhte hain ki kaunse gaane log aksar ek saath sunte hain playlists mein. Jo gaane ek saath aate hain, woh shayad meaning mein similar honge (jaise ek type ke honge - rock, pop, sad, happy)।

Hum ek dataset use karenge jismein user playlists hain (sirf song IDs ki list), aur phir uspar ek Word2Vec jaisa model train karenge। Model har song ID ko ek meaning number (embedding) dega, aur phir hum similar numbers wale songs dhundh kar recommend karenge।

### Code: Song Playlist Data Load Karna

Hum ek online dataset download karenge jismein bahut saari song playlists hain (har playlist mein song IDs ki list)।

```python
# Zaroori tools laate hain: pandas (data tables ke liye) aur urllib (online file download ke liye).\
import pandas as pd
from urllib import request

# Online se playlist dataset file download karte hain.\
# request.urlopen() online file open karta hai.\
data = request.urlopen('https://storage.googleapis.com/maps-premium/dataset/yes_complete/train.txt')

# Downloaded file ko read karte hain, bytes se text mein badalte hain (.decode(\"utf-8\")), lines mein todte hain (.split('\\n')).\
# Shuru ki do lines mein extra info hai, unko chhod dete hain [2:] se.\
lines = data.read().decode("utf-8").split('\\n')[2:]

# Har line (playlist) ko chote numbers (song IDs) mein todte hain.\
# s.rstrip().split() line ke end se extra space hatata hai aur words (IDs) mein todta hai.\
# List comprehension [...] for ... if ... use karke hum sirf woh playlists rakhte hain jismein 1 se zyada songs hain (len(s.split()) > 1).\
playlists = [s.rstrip().split() for s in lines if len(s.split()) > 1]

# Ab song ki details (naam, artist) wali file load karte hain.\
# Online se file download karo, read karo, decode karo, lines mein todo.\
songs_file = request.urlopen('https://storage.googleapis.com/maps-premium/dataset/yes_complete/song_hash.txt')
songs_file = songs_file.read().decode("utf-8").split('\\n')
# Har line ko song ID, title, artist mein todo (split('\\t') tab character par todta hai).\
songs = [s.rstrip().split('\\t') for s in songs_file]
# pandas DataFrame mein daalo, columns ke naam do.\
songs_df = pd.DataFrame(data=songs, columns = ['id', 'title', 'artist'])
# Song ID ko index bana do taaki ID se details quickly dhundh sakein.\
songs_df = songs_df.set_index('id')

# Data load ho gaya! Playlists list mein hain aur song details songs_df mein.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code ek online dataset download karta hai jismein user playlists (`playlists`) aur song details (`songs_df`) hain. Playlists mein sirf song IDs ki lists hain, aur song details mein har ID ke liye song ka naam aur artist hai. Hum is data ka use karke seekhenge ki kaise songs ko embeddings mein badal kar recommendations banate hain।

### Code: Sample Playlists Dekhna

Load kiye hue playlists kaise dikhte hain, chalo dekhte hain।

```python
# Load kiye hue playlists mein se pehle 2 playlists dekhte hain.\
# playlists[0] pehli playlist hai, playlists[1] doosri.\
# print function se screen par dikhao.\
print( 'Playlist #1:\\n ', playlists[0], '\\n')
print( 'Playlist #2:\\n ', playlists[1])

# Output mein dekho, yeh numbers (song IDs) ki lambi lambi lists hain.\
# Har list ek user ki playlist hai.\
# Model in lists ko padh kar seekhega ki kaunse song IDs (songs) aksar ek saath aate hain.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code `playlists` list ke pehle do items print karta hai. Yeh dikhata hai ki playlist data kaisa dikhta hai - song IDs ki lists. Har list ek user ki playlist ko represent karti hai. Yahi sequences hain jinpar hum apna song embedding model train karenge।

### Code: Playlists Par Naya Embedding Model (Word2Vec) Train Karna

Ab hum playlists ke data par **Word2Vec** naam ka ek embedding model train karenge. Yeh model playlists ko padhega aur har song ID ke liye ek \"meaning number\" (embedding) banayega. Jo songs ek hi playlist mein ya aas paas aate hain, unke embeddings similar banenge।

💡 **Analogy:** Socho, \"king\" aur \"queen\" shabdon ke Word2Vec embeddings similar hote hain kyunki woh aksar ek saath aate hain (jaise sentences mein). Waise hi, agar log \"Song A\" aur \"Song B\" ko apni playlists mein aksar ek saath rakhte hain, toh Word2Vec \"Song A\" ID aur \"Song B\" ID ke embeddings ko close (similar) bana dega।

```python
# gensim.models se Word2Vec tool laate hain.\
from gensim.models import Word2Vec

# Ab hamara Word2Vec model train karte hain.\
# Word2Vec(...) se model banate hain.\
# playlists: Yeh hamara data hai (lists of song IDs), jisko model padhega.\
# vector_size=32: Har song ID ke liye 32 numbers ka vector banega (embedding size).\
# window=20: Model dekhega ki ek song ke aas paas 20 songs tak kaunse songs aate hain (context window).\
# negative=50: Training ke liye ek technique jo model ko improve karti hai.\
# min_count=1: Jo song ID kam se kam 1 baar playlist mein aaya hai, uska embedding banega.\
# workers=4: Training mein 4 CPU cores use karo (agar available hon) taaki tez ho.\
model = Word2Vec(\
    playlists, vector_size=32, window=20, negative=50, min_count=1, workers=4\
)

# Model train ho gaya! Ab har song ID ke liye hamare paas ek 32 numbers ka embedding hai.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code `gensim` library ka Word2Vec algorithm use karke hamare `playlists` data par ek naya embedding model train karta hai. Word2Vec har unique song ID ko ek 32-dimensional numerical vector (embedding) assign karta hai. Training ka goal hota hai ki jo song IDs (songs) playlists mein aksar ek doosre ke paas aate hain, unke vectors bhi numerical space mein ek doosre ke paas hon।

### Code: Train Kiye Model Se Similar Song IDs Dhundhna

Ab jo model train hua hai, usse hum kisi song ID ke sabse similar song IDs pooch sakte hain। Yeh similar IDs woh hongi jinke embeddings numerical space mein given song ID ke embedding ke sabse paas hon।

```python
# Ek song ID choose karte hain recommendations dekhne ke liye.\
# Yeh \"Fade To Black\" by Metallica hai.\
song_id = 2172

# Model se poochhte hain ki song ID 2172 ke sabse similar 10 song IDs kaunsi hain.\
# model.wv: Yeh trained model ke word vectors (embeddings) ka access deta hai.\
# .most_similar(positive=str(song_id)): song_id (string format mein) ke vector ke similar vectors dhundho.\
# topn=10: Sabse similar 10 vectors batao.\
model.wv.most_similar(positive=str(song_id))

# Output mein dekho, yeh 10 song IDs ki list hai, saath mein similarity score bhi hai.\
# Yeh woh songs hain jinke embeddings song 2172 ke embedding ke sabse zyada similar hain.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code hamare train kiye hue Word2Vec `model` ka `most_similar` function use karke choose kiye hue `song_id` (2172) ke embedding vector ke numerical space mein sabse paas wale 10 song ID vectors dhundhta hai. Output mein un song IDs ki list aati hai, jo Word2Vec ke hisaab se given song ke similar hain (kyunki woh playlists mein aksar saath dikhte the)।

### Code: Original Song Ke Details Dekhna

Song ID 2172 kya tha, yeh yaad nahi hai? Chalo uski details dekhte hain hamare `songs_df` (DataFrame) se।

```python
# song ID 2172 ki details (title aur artist) dekhte hain songs_df se.\
# songs_df.iloc[] se hum index use karke row nikal sakte hain.\
# Hum 2172 ko string format mein de rahe hain kyunki DataFrame ka index string hai.\
print(songs_df.iloc[2172])

# Output mein dekho, yeh \"Fade To Black\" by Metallica tha. Ab recommendations samajhna aasan hoga!
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code `songs_df` DataFrame ka use karke `song_id` 2172 ke details (title aur artist) print karta hai. Kyunki humne `song_hash.txt` file ko load karte waqt song ID ko index banaya tha, hum `songs_df.iloc[2172]` se us song ki row easily nikal sakte hain. Isse humein pata chalta hai ki hum kis original song ke liye recommendations dekh rahe hain।

### Code: Recommendations Dikhane Wala Function Banana

Ab recommendations dhundhne (using Word2Vec) aur unki details dikhane (using DataFrame) ke steps ko ek function mein daalte hain. Yeh function kisi bhi song ID ke liye recommendations dikhayega।

```python
# numpy library import karte hain calculations ke liye.\
import numpy as np

# Yeh function kisi bhi song ID ke liye recommendations dhundh kar unki details dikhayega.\
# Input mein song_id lega.\
def print_recommendations(song_id):
    # model.wv.most_similar se similar songs ke IDs aur scores milte hain.\
    # np.array(...) usko numpy array mein badalta hai.\
    # [:,0] matlab array ke har row ka pehla item lo (jo ki song ID hai), scores ko ignore karo.\
    # str(song_id) song ID ko string mein badalta hai kyunki model string IDs use karta hai.\
    # topn=5 matlab top 5 similar songs chahiye.\
    similar_songs = np.array(\
        model.wv.most_similar(positive=str(song_id),topn=5)\
    )[:,0]
    # Ab songs_df.iloc[] use karke un similar song IDs ki details (title, artist) nikalte hain.\
    return  songs_df.iloc[similar_songs]

# Function taiyaar hai! Ab isko use kar sakte hain.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code `print_recommendations` naam ka ek function banata hai. Yeh function ek song ID input leta hai. Us ID ko string mein badal kar `model.wv.most_similar` se top 5 similar song IDs dhundhta hai. Phir numpy array use karke sirf IDs nikal leta hai (similarity scores ko chhod kar). Finally, `songs_df.iloc[]` ka use karke un 5 recommended song IDs ki details (title, artist) nikal kar wapas karta hai। Yeh function hamara recommendation logic hai।

### Code: Song 2172 Ke Liye Recommendations Dekhna

Ab recommendation function ko use karke dekhte hain ki song ID 2172 (\"Fade To Black\" by Metallica) ke liye kya recommendations aate hain।

```python
# Recommendation function ko song ID 2172 do aur uska output print karo.\
# Is function ke andar similar song IDs dhundh kar unki details nikal kar return hongi.\
print_recommendations(2172)

# Output mein dekho! Top 5 songs aa gaye jo Word2Vec ke hisaab se \"Fade To Black\" by Metallica ke similar hain.\
# Jaise \"Run To The Hills\" (Iron Maiden), \"Red Barchetta\" (Rush). Yeh sab classic rock/metal songs hain.\
# Iska matlab hai ki Word2Vec ne playlists ke data se gaano ka style ya mood capture kar liya! Cool na?
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code hamare banaye hue `print_recommendations` function ko `song_id` 2172 dekar run karta hai. Function Word2Vec model use karke song 2172 ke similar song IDs dhundhta hai, aur phir `songs_df` se un song IDs ke titles aur artists nikal kar DataFrame format mein print karta hai. Output mein jo songs dikhte hain, woh Word2Vec model ke train kiye hue embeddings ke hisaab se "Fade To Black" ke similar hain, jo dikhata hai ki embeddings recommendation system mein kaise kaam kar sakte hain।

### Code: Song 842 Ke Liye Recommendations Dekhna

Ek aur song ID try karte hain recommendations dekhne ke liye। Song ID 842 hai \"California Love\" by 2Pac।

```python
# Recommendation function ko song ID 842 do aur uska output print karo.\
# Dekhte hain Hip-Hop song ke liye kya recommendations aate hain.\
print_recommendations(842)

# Output mein dekho! Ab recommendations Hip-Hop ke context mein aa rahe hain.\
# Jaise \"How We Do\" (The Game), \"If I Ruled The World\" (Nas), \"Heartless\" (Kanye West).\
# Yeh dikhata hai ki embeddings sirf music style hi nahi, balki sub-genres aur related artists/songs ko bhi capture kar sakte hain!\
# Yahi hai embeddings ka jaadu - shabdon ya items ke matlab ko numbers mein badal kar unke beech ke rishte samajhna.
```

**Yeh Code Kya Karta Hai? 🤔**

Yeh code `print_recommendations` function ko `song_id` 842 dekar run karta hai. Output mein jo songs recommend hote hain, woh Word2Vec model ke hisaab se "California Love" (2Pac) ke similar hain. Jab hum recommendations dekhte hain (jaise The Game, Nas, Kanye West), toh humein pata chalta hai ki yeh bhi Hip-Hop artists hain. Iska matlab hai ki Word2Vec model playlists ke data se seekh kar songs ke style ya genre ko bhi embeddings mein capture kar leta hai, jisse relevant recommendations milte hain।

---

## Seekhe Hue Shabd (Glossary) 📚

Chalo, jo naye aur important technical shabd humne is Chapter mein seekhe, unka matlab aur thoda simple explanation aur analogies dekh lete hain:

*   **Tokens:** Bhasha (text) ke chote chote tukde jinmein AI model input ko todta hai. Yeh poore shabd ho sakte hain, shabdon ke hisse (`apolog`, `izing`), punctuation (`.`, `:`), ya special symbols/characters। **Analogy:** Jaise building blocks ya LEGO pieces jinse poora sentence banta hai।
*   **Tokenization:** Woh process jismein Language Model ka tokenizer input text ko in chote chote **Tokens** mein todta hai। **Analogy:** Jaise koi cheez ko chote chote parts mein divide karna usko study karne ya use karne ke liye।
*   **Token ID:** Har unique token ke liye ek special number. AI model tokens ko unke IDs se pehchanta hai aur numbers par kaam karta hai। **Analogy:** Jaise har LEGO piece ka apna ek unique number ya code ho।
*   **Embeddings:** Tokens (ya poore sentences/documents) ko represent karne wali numbers ki list (vector). Yeh numbers token/text ke "matlab" ya meaning ko capture karte hain। **Analogy:** Har LEGO piece ka ek "power level" ya "functionality score" list, jo batata hai ki woh kis tarah ka piece hai aur kya kar sakta hai।
*   **Contextualized Embeddings:** Modern LLMs dwara banaye gaye embeddings jahan ek token ka meaning number uske aas paas ke shabdon (context) par depend karta hai। **Analogy:** Jaise \"bank\" shabd ka meaning number list sentence ke hisaab se badal jayega।
*   **Text Embeddings / Sentence Embeddings:** Ek single meaning number list jo poore sentence ya poore document ke combined matlab ko represent karta hai। **Analogy:** Jaise poore LEGO model ka ek overall score jo batata hai ki woh kis tarah ka model hai (car, building, etc.)।
*   **Non-Contextual Embeddings:** Purane tarike ke embeddings jahan ek word ka meaning number hamesha same rehta hai, bhale hi woh kisi bhi context mein ho। **Analogy:** Jaise purani dictionary mein har word ka ek hi entry ho।
*   **Word2Vec:** Non-Contextual Word Embeddings banane ka ek popular algorithm jo shabdon ko unke aas paas aane wale shabdon ke hisaab se numbers deta hai। **Analogy:** Jaise shabdon ki dosti ka score: jo shabd dost hain (aksar saath aate hain), unke numbers paas paas honge।
*   **GloVe:** Non-Contextual Word Embeddings banane ka ek aur popular algorithm. Yeh World2Vec se thoda alag tarike se kaam karta hai par idea similar hai। **Analogy:** Dosti ka score calculate karne ka ek doosra tarika।
*   **Gensim:** Ek Python library jo Word Embeddings (jaise Word2Vec, GloVe) aur related text processing tasks ke liye tools deta hai। **Analogy:** Ek toolkit jismein Word Embeddings banane aur use karne ke saare auzaar hain।
*   **DataFrame (Pandas):** Data ko rows aur columns mein organize karne ka ek structured tarika, jaise ek smart spreadsheet table Python mein। **Analogy:** Ek organized table jismein songs ki IDs ke saath unke naam aur artist likhe hain, aur hum ID se jaldi dhundh sakte hain।

---

## Summary: Kya Seekha Aur Aage Kya? 🎉

Waah! Aaj humne AI ke andar ke kuch bahut important concepts ko explore kiya:

*   Humne samjha ki AI models hamari bhasha ko chote chote **Tokens** mein todte hain (using a **Tokenizer**), aur har token ka ek **Token ID** hota hai।
*   Humne dekha ki alag alag models ke **Tokenizers** ek hi text ko alag alag tarike se handle karte hain (capitalization, spaces, special chars)।
*   Humne seekha ki **Embeddings** kya hote hain - tokens ya text ko represent karne wale meaning numbers।
*   Humne **Contextualized Embeddings** (jaise BERT/DeBERTa se) ko dekha, jahan meaning numbers context ke hisaab se badalte hain।
*   Humne **Text Embeddings** (Sentence-BERT se) ko dekha, jo poore sentence ka ek single meaning number dete hain।
*   Humne **Non-Contextual Embeddings** (jaise Word2Vec/GloVe) ko dekha, jo LLMs se pehle aate the aur jahan word ka embedding hamesha same rehta hai।
*   Aur sabse mazedaar baat, humne dekha ki kaise **embeddings** ka use karke hum song recommendations bana sakte hain, yeh dikhata hai ki meaning numbers kitne useful ho sakte hain real-world applications mein!

Yeh Chapter AI ke Language understanding ki foundation hai. Tokens aur Embeddings woh tarika hai jisse computer hamari baaton ko numerical roop deta hai jispar calculations ki ja sakein।

Aage chapters mein, hum Language Models ke aur bhi andar jaayenge, unke architecture (woh kaise bane hain) ko samjhenge, aur dekhenge ki kaise woh in embeddings ka use karke itne smart answers generate karte hain!

Keep building with AI's LEGO blocks! 🧱🤖

---