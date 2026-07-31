[index.html.html](https://github.com/user-attachments/files/30595234/index.html.html)
<!DOCTYPE html>
<html lang="zh">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>旅客高频问答库 | 国风华裳主题航班</title>
    <style>
        :root {
            --bg: #f9f3e9;
            --card: #fffef8;
            --primary: #1a3c5e;
            --gold: #c9a24e;
            --gold-light: #e0c87a;
            --text: #2c1f0e;
            --text-light: #6b5c4a;
            --border: #d4c5a8;
            --shadow: 0 4px 16px rgba(100, 70, 30, 0.08);
            --radius: 16px;
        }
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'PingFang SC', 'Microsoft YaHei', 'STSong', 'SimSun', sans-serif;
            background: #1a1a2e;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 6px;
            color: var(--text);
        }
        .app {
            width: 100%;
            max-width: 540px;
            height: 96vh;
            max-height: 900px;
            background: var(--bg);
            border-radius: 28px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4), inset 0 0 0 3px #3a2a1a;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }
        .header {
            background: var(--primary);
            color: #e0c87a;
            padding: 14px 16px;
            text-align: center;
            flex-shrink: 0;
            letter-spacing: 1px;
        }
        .header h1 {
            font-size: 18px;
            font-weight: 700;
        }
        .header .sub {
            font-size: 11px;
            opacity: 0.8;
            margin-top: 3px;
        }
        .content {
            flex: 1;
            overflow-y: auto;
            padding: 14px;
            -webkit-overflow-scrolling: touch;
        }
        .content::-webkit-scrollbar {
            width: 3px;
        }
        .content::-webkit-scrollbar-thumb {
            background: var(--gold);
            border-radius: 3px;
        }
        .search-wrap {
            position: relative;
            margin-bottom: 12px;
        }
        .search-input {
            width: 100%;
            padding: 10px 40px 10px 16px;
            border: 2px solid var(--border);
            border-radius: 28px;
            font-size: 14px;
            background: var(--card);
            font-family: inherit;
            color: var(--text);
            transition: 0.2s;
        }
        .search-input:focus {
            border-color: var(--gold);
            outline: none;
        }
        .search-icon {
            position: absolute;
            right: 14px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 16px;
            color: var(--text-light);
            pointer-events: none;
        }
        .tag-row {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
            margin-bottom: 14px;
        }
        .filter-tag {
            padding: 6px 14px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
            cursor: pointer;
            border: 1px solid var(--border);
            background: var(--card);
            color: var(--text-light);
            transition: all 0.2s;
        }
        .filter-tag.active {
            background: var(--primary);
            color: #fff;
            border-color: var(--primary);
        }
        .filter-tag:hover {
            border-color: var(--gold);
        }
        .faq-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .faq-item {
            background: var(--card);
            border-radius: var(--radius);
            border: 1px solid var(--border);
            box-shadow: var(--shadow);
            overflow: hidden;
            transition: all 0.25s;
        }
        .faq-item.hidden {
            display: none;
        }
        .faq-question {
            display: flex;
            align-items: flex-start;
            gap: 10px;
            padding: 14px 15px;
            cursor: pointer;
            user-select: none;
            transition: background 0.2s;
        }
        .faq-question:hover {
            background: #fef9f0;
        }
        .q-icon {
            width: 32px;
            height: 32px;
            border-radius: 50%;
            background: var(--primary);
            color: #fff;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 800;
            font-size: 13px;
            flex-shrink: 0;
        }
        .q-content {
            flex: 1;
            min-width: 0;
        }
        .q-title {
            font-size: 14px;
            font-weight: 700;
            color: var(--text);
            line-height: 1.5;
        }
        .q-category {
            display: inline-block;
            font-size: 10px;
            padding: 2px 8px;
            border-radius: 10px;
            font-weight: 600;
            margin-top: 4px;
        }
        .cat-hanfu {
            background: #e8f0f8;
            color: #1a3c5e;
        }
        .cat-qipao {
            background: #fdf0e0;
            color: #8b5a2b;
        }
        .cat-culture {
            background: #e8f5e9;
            color: #2e5a30;
        }
        .cat-service {
            background: #f3e8f8;
            color: #4a2e6e;
        }
        .cat-souvenir {
            background: #fff3e0;
            color: #e65100;
        }
        .cat-fabric {
            background: #fce4ec;
            color: #880e4f;
        }
        .q-arrow {
            font-size: 18px;
            color: var(--gold);
            transition: transform 0.3s;
            flex-shrink: 0;
            margin-top: 2px;
        }
        .faq-item.open .q-arrow {
            transform: rotate(180deg);
        }
        .faq-answer {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease, padding 0.3s;
            background: #fdf8f0;
            border-top: 1px dashed var(--border);
        }
        .faq-item.open .faq-answer {
            max-height: 800px;
            padding: 14px 15px;
        }
        .answer-en {
            font-size: 14px;
            line-height: 1.7;
            color: var(--text);
            margin-bottom: 6px;
        }
        .answer-zh {
            font-size: 12px;
            color: var(--text-light);
            line-height: 1.6;
            font-style: italic;
            margin-bottom: 8px;
        }
        .cultural-tip {
            background: #fff9e0;
            border-left: 4px solid var(--gold);
            padding: 10px 14px;
            border-radius: 8px;
            margin: 8px 0;
            font-size: 12px;
            color: #5a4a30;
            line-height: 1.6;
        }
        .cultural-tip .tip-icon {
            font-size: 14px;
            margin-right: 4px;
        }
        .audio-btn {
            display: inline-flex;
            align-items: center;
            gap: 4px;
            background: var(--gold);
            color: #fff;
            border: none;
            border-radius: 16px;
            padding: 5px 12px;
            font-size: 12px;
            cursor: pointer;
            margin-top: 6px;
            font-weight: 600;
            transition: 0.2s;
        }
        .audio-btn:hover {
            background: #b3824a;
        }
        .audio-btn.playing {
            background: #b8443c;
        }
        .empty-state {
            text-align: center;
            padding: 30px;
            color: var(--text-light);
        }
        .empty-state .icon {
            font-size: 40px;
            display: block;
            margin-bottom: 8px;
        }
        .footer-info {
            text-align: center;
            padding: 8px;
            font-size: 11px;
            color: var(--text-light);
            border-top: 1px dashed var(--border);
            margin-top: 8px;
        }
        @media (max-width: 380px) {
            .q-title {
                font-size: 13px;
            }
            .answer-en {
                font-size: 13px;
            }
        }
    </style>
</head>
<body>
    <div class="app">
        <div class="header">
            <h1>🪶 旅客高频问答库</h1>
            <div class="sub">Chinese Costume Theme Flight · FAQ</div>
        </div>
        <div class="content">
            <div class="search-wrap">
                <input type="text" class="search-input" id="searchInput" placeholder="搜索问题... (支持中英文)" autocomplete="off">
                <span class="search-icon">🔍</span>
            </div>
            <div class="tag-row" id="tagRow">
                <span class="filter-tag active" data-cat="all">全部</span>
                <span class="filter-tag" data-cat="hanfu">👘 汉服</span>
                <span class="filter-tag" data-cat="qipao">👗 旗袍</span>
                <span class="filter-tag" data-cat="culture">🏛 文化寓意</span>
                <span class="filter-tag" data-cat="service">✈️ 客舱服务</span>
                <span class="filter-tag" data-cat="souvenir">🛍️ 文创产品</span>
                <span class="filter-tag" data-cat="fabric">🧵 面料工艺</span>
            </div>
            <div class="faq-list" id="faqList"></div>
            <div class="footer-info">
                📋 共 <b id="faqCount">15</b> 个常见问题 · 点击问题展开查看标准回答
            </div>
        </div>
    </div>
    <script>
        (function() {
            const faqData = [{
                id: 1,
                question: 'What is Hanfu?',
                questionZh: '什么是汉服？',
                answerEn: 'Hanfu is the traditional costume of the Han ethnic group in China, with a history of thousands of years. It is known for its elegant features, such as cross-collars, wide sleeves, and a flowing robe.',
                answerZh: '汉服是中国汉民族的传统服饰，拥有数千年历史。它以交领、广袖、飘逸的袍服等优雅特征而闻名。',
                culturalTip: 'Hanfu is not just clothing — it embodies the Confucian ideals of harmony and propriety. The cross-collar (交领) wrapping to the right (右衽) was a key cultural symbol distinguishing Chinese civilization from neighboring cultures.',
                category: 'hanfu',
                categoryLabel: '汉服',
                catClass: 'cat-hanfu',
                tags: ['汉服', '定义', 'Hanfu', 'traditional costume']
            }, {
                id: 2,
                question: 'Is Cheongsam (Qipao) a type of Hanfu?',
                questionZh: '旗袍是汉服的一种吗？',
                answerEn: 'Cheongsam, or Qipao, is a beautiful and classic Chinese traditional costume, but it is different from Hanfu. It was developed in the early 20th century and has its own unique style, while Hanfu refers to the clothing system of the Han people before the Qing Dynasty.',
                answerZh: '旗袍是美丽经典的中国传统服饰，但与汉服不同。旗袍发展于20世纪初，有其独特风格；而汉服指清代以前汉民族的服饰体系。',
                culturalTip: 'Qipao evolved from the Manchu "changpao" and was modernized in 1920s Shanghai, blending Eastern and Western fashion. Hanfu, by contrast, dates back over 3,000 years and was the dominant clothing before the Qing Dynasty.',
                category: 'qipao',
                categoryLabel: '旗袍',
                catClass: 'cat-qipao',
                tags: ['旗袍', 'Qipao', 'Cheongsam', '区别', '汉服']
            }, {
                id: 3,
                question: 'What do the cloud patterns in the cabin represent?',
                questionZh: '客舱里的祥云图案代表什么？',
                answerEn: 'The cloud patterns are traditional Chinese auspicious symbols. They represent good luck, happiness, and peace. We hope these beautiful patterns bring you a pleasant and auspicious journey.',
                answerZh: '祥云图案是中国传统吉祥符号，代表好运、幸福与平安。我们希望这些美丽的图案为您带来愉快吉祥的旅程。',
                culturalTip: 'Cloud patterns (祥云纹) have been used in Chinese art for over 2,000 years. They symbolize the connection between heaven and earth, and are often paired with dragons or cranes to represent divine blessings.',
                category: 'culture',
                categoryLabel: '文化寓意',
                catClass: 'cat-culture',
                tags: ['祥云', 'cloud pattern', '装饰', '寓意', '吉祥']
            }, {
                id: 4,
                question: 'Can I take photos with the Hanfu display?',
                questionZh: '我可以和汉服展示拍照吗？',
                answerEn: 'Absolutely! You are more than welcome to take photos with the Hanfu display. We hope you enjoy the unique cultural atmosphere on our flight.',
                answerZh: '当然可以！非常欢迎您与汉服展示拍照留念。希望您享受我们航班上独特的文化氛围。',
                culturalTip: 'Taking photos helps share Chinese culture with the world. Feel free to ask our crew to take a photo for you — we are happy to help capture your special moment on this themed flight.',
                category: 'service',
                categoryLabel: '客舱服务',
                catClass: 'cat-service',
                tags: ['拍照', 'photo', '展示', '体验', '服务']
            }, {
                id: 5,
                question: 'When do people in China wear Hanfu nowadays?',
                questionZh: '现在中国人什么时候穿汉服？',
                answerEn: 'Today, Hanfu is often worn during traditional festivals, cultural events, weddings, or for special occasions to celebrate and inherit Chinese culture. It\'s a way for people to connect with their heritage.',
                answerZh: '如今，汉服常在传统节日、文化活动、婚礼或特殊场合穿着，以庆祝和传承中国文化。这是人们连接传统的一种方式。',
                culturalTip: 'The modern "Hanfu revival movement" began in the early 2000s among young people eager to reconnect with their cultural roots. Today, millions participate in Hanfu festivals like the annual "Hanfu Day" celebrations.',
                category: 'hanfu',
                categoryLabel: '汉服',
                catClass: 'cat-hanfu',
                tags: ['汉服', '穿着场合', '节日', '文化传承']
            }, {
                id: 6,
                question: 'Where can I buy the souvenirs I see on the plane?',
                questionZh: '我在飞机上看到的纪念品在哪里可以购买？',
                answerEn: 'We have a selection of exquisite Hanfu-themed souvenirs available for purchase on board. You can find the order form in the in-flight magazine, or simply ask any flight attendant for assistance.',
                answerZh: '我们精选了一系列汉服主题文创纪念品，可在机上购买。您可以在客舱杂志中找到订购单，或直接向任何乘务员寻求帮助。',
                culturalTip: 'Our souvenirs are designed in collaboration with intangible cultural heritage artisans. Each piece — from silk scarves to embroidered pouches — carries a unique story of Chinese craftsmanship.',
                category: 'souvenir',
                categoryLabel: '文创产品',
                catClass: 'cat-souvenir',
                tags: ['纪念品', 'souvenir', '购买', '文创', '购物']
            }, {
                id: 7,
                question: 'What is the meaning of the peony embroidery?',
                questionZh: '牡丹刺绣有什么寓意？',
                answerEn: 'The peony is known as the "king of flowers" in China. It symbolizes prosperity, wealth, and honor. The beautiful peony embroidery you see is a wish for a prosperous and happy life.',
                answerZh: '牡丹在中国被誉为"花中之王"，象征繁荣、富贵和尊荣。您看到的精美牡丹刺绣寄托了对繁荣幸福生活的祝愿。',
                culturalTip: 'Peonies were the national flower of the Tang Dynasty and appear in countless poems and paintings. In embroidery, peonies are often combined with butterflies or phoenixes to symbolize love and harmony.',
                category: 'culture',
                categoryLabel: '文化寓意',
                catClass: 'cat-culture',
                tags: ['牡丹', 'peony', '刺绣', '寓意', '富贵']
            }, {
                id: 8,
                question: 'Are there any cultural activities on this flight?',
                questionZh: '这个航班上有文化活动吗？',
                answerEn: 'Yes! We will be holding a small Hanfu culture quiz later. It\'s a fun way to learn more about traditional Chinese costumes, and there are small gifts for the winners. We hope you can join us.',
                answerZh: '有的！稍后我们将举办小型汉服文化问答活动。这是了解中国传统服饰的有趣方式，获胜者还有小礼品。期待您的参与！',
                culturalTip: 'In addition to the quiz, we also offer a Hanfu try-on experience at the rear cabin. You can wear a Tang suit or Ming-style Hanfu and take memorable photos during the flight.',
                category: 'service',
                categoryLabel: '客舱服务',
                catClass: 'cat-service',
                tags: ['活动', 'quiz', '互动', '文化问答', '服务']
            }, {
                id: 9,
                question: 'What cultural and creative products are available on this flight?',
                questionZh: '这次航班上有什么文创产品？',
                answerEn: 'We offer a variety of Hanfu-themed cultural and creative products, including silk scarves with cloud brocade patterns, embroidered pouches, Hanfu-style bookmarks, and traditional tassel keychains. Each item is designed with authentic Chinese cultural elements.',
                answerZh: '我们提供多种汉服主题文创产品，包括云锦纹样丝巾、刺绣荷包、汉服元素书签和传统流苏钥匙扣。每件产品都融入了地道的中式文化元素。',
                culturalTip: 'Our cultural products are not just souvenirs — they are carriers of intangible cultural heritage. The cloud brocade (云锦) pattern on our silk scarves is recognized as a national-level intangible cultural heritage, often called "inch of brocade, inch of gold".',
                category: 'souvenir',
                categoryLabel: '文创产品',
                catClass: 'cat-souvenir',
                tags: ['文创产品', 'cultural products', '丝巾', '荷包', '购物']
            }, {
                id: 10,
                question: 'How can I tell different dynasties\' Hanfu apart?',
                questionZh: '如何区分不同朝代的汉服？',
                answerEn: 'Generally, Tang-style Hanfu is bold and colorful with wide sleeves; Song-style is more restrained and slim-fitting; Ming-style features elaborate embroidery and a dignified silhouette. Each dynasty had its own aesthetic preferences.',
                answerZh: '大致来说，唐制汉服色彩大胆、袖口宽大；宋制则更为内敛修身；明制以精美刺绣和端庄版型著称。每个朝代都有独特的审美风格。',
                culturalTip: 'The Tang Dynasty (618-907) was an open, cosmopolitan era, reflected in its bright colors and foreign influences. The Song (960-1279) favored understated elegance, while the Ming (1368-1644) emphasized grandeur and intricate embroidery.',
                category: 'hanfu',
                categoryLabel: '汉服',
                catClass: 'cat-hanfu',
                tags: ['朝代', 'dynasty', '唐制', '宋制', '明制', '区分']
            }, {
                id: 11,
                question: 'What is cloud brocade and why is it special?',
                questionZh: '什么是云锦？它为什么特别？',
                answerEn: 'Cloud brocade (Yunjin) is a luxurious traditional Chinese silk fabric with a history of over 1,600 years. It is recognized as a national intangible cultural heritage. The weaving technique is so complex that a skilled artisan can only produce 5-6 centimeters per day.',
                answerZh: '云锦是一种奢华的中国传统丝织品，已有1600多年历史，被认定为国家级非物质文化遗产。其织造工艺极为复杂，熟练工匠每天仅能织出5-6厘米。',
                culturalTip: 'The name "cloud brocade" comes from its brilliant, cloud-like patterns woven with gold and silver threads. It was exclusively used by the imperial family during the Yuan, Ming, and Qing Dynasties. There is a famous saying: "An inch of cloud brocade is worth an inch of gold."',
                category: 'fabric',
                categoryLabel: '面料工艺',
                catClass: 'cat-fabric',
                tags: ['云锦', 'cloud brocade', '面料', '非遗', '丝绸']
            }, {
                id: 12,
                question: 'Why does Hanfu have a cross-collar that wraps to the right?',
                questionZh: '为什么汉服是交领右衽？',
                answerEn: 'The cross-collar wrapping to the right (youren) is a defining feature of Hanfu. It reflects the Chinese cultural value of "righteousness" and was historically used to distinguish Chinese civilization — the Han people wore the collar wrapping right, while some neighboring cultures wrapped left.',
                answerZh: '交领右衽是汉服的核心特征。它体现了中国文化中"正"的价值观念，历史上用于区分华夏与周边文化——汉人右衽，而部分周边族群左衽。',
                culturalTip: 'The "left vs. right" collar distinction was so culturally significant that Confucius once praised a minister for preserving the right-wrapping tradition, saying "But for him, we might now be wearing our collars folded to the left."',
                category: 'culture',
                categoryLabel: '文化寓意',
                catClass: 'cat-culture',
                tags: ['交领', 'cross-collar', '右衽', '文化', '礼仪']
            }, {
                id: 13,
                question: 'Can I try on Hanfu during the flight?',
                questionZh: '我可以在航班上试穿汉服吗？',
                answerEn: 'Yes! We have a Hanfu try-on corner at the rear galley. You can choose from several styles including Tang suit and Ming-style Hanfu. Our crew will be happy to help you put it on and take photos.',
                answerZh: '可以！我们在客舱后部设有汉服试穿区。您可以选择唐装、明制汉服等几种款式。我们的乘务员很乐意帮您穿戴并拍照。',
                culturalTip: 'The try-on experience is designed to give you a hands-on appreciation of traditional Chinese clothing. Many passengers say it is the highlight of their flight — a unique memory above the clouds.',
                category: 'service',
                categoryLabel: '客舱服务',
                catClass: 'cat-service',
                tags: ['试穿', 'try-on', '体验', '拍照', '服务']
            }, {
                id: 14,
                question: 'What is the difference between Hanfu and Kimono?',
                questionZh: '汉服和和服有什么区别？',
                answerEn: 'While both are beautiful East Asian traditional costumes, Hanfu originated in China over 3,000 years ago, while the kimono evolved from Hanfu influences during the Tang Dynasty. Hanfu typically has a cross-collar and flowing sleeves, while the kimono has a wider obi belt and a more structured silhouette.',
                answerZh: '两者都是美丽的东亚传统服饰，但汉服起源于3000多年前的中国，而和服是在唐代受汉服影响演变而来。汉服通常是交领和飘逸广袖，和服则有更宽的腰带和更硬挺的廓形。',
                culturalTip: 'Hanfu significantly influenced the clothing of neighboring countries including Japan, Korea, and Vietnam. The kimono\'s prototype was directly inspired by Tang Dynasty court dress brought back by Japanese envoys.',
                category: 'hanfu',
                categoryLabel: '汉服',
                catClass: 'cat-hanfu',
                tags: ['汉服', '和服', 'kimono', '区别', '对比']
            }, {
                id: 15,
                question: 'How should I choose a souvenir as a gift?',
                questionZh: '如何选择合适的纪念品作为礼物？',
                answerEn: 'It depends on the recipient. Silk scarves with peony patterns are perfect for those who appreciate elegance; embroidered pouches make lovely gifts for friends; and Hanfu bookmarks are ideal for book lovers. Each item comes with a card explaining its cultural meaning.',
                answerZh: '这取决于送礼对象。牡丹纹样丝巾适合喜爱优雅风格的人；刺绣荷包是送给朋友的美好礼物；汉服书签则是爱书人的理想选择。每件产品都附有文化含义说明卡。',
                culturalTip: 'In Chinese gift-giving culture, the symbolism of the pattern matters greatly. Peonies represent wealth and honor, clouds symbolize good fortune, and the combination of both conveys the wish for a prosperous and peaceful life.',
                category: 'souvenir',
                categoryLabel: '文创产品',
                catClass: 'cat-souvenir',
                tags: ['礼物', 'gift', '选购', '丝巾', '荷包', '书签']
            }];

            let activeCat = 'all';
            let searchTerm = '';
            const $ = id => document.getElementById(id);
            const faqList = $('faqList');
            const searchInput = $('searchInput');
            const faqCount = $('faqCount');

            function speakTTS(text, btn) {
                const synth = window.speechSynthesis;
                if (!synth) return;
                if (btn) btn.classList.remove('playing');
                synth.cancel();
                const utterance = new SpeechSynthesisUtterance(text);
                utterance.lang = 'en-US';
                utterance.rate = 0.88;
                utterance.volume = 1;
                if (btn) {
                    btn.classList.add('playing');
                    utterance.onend = () => btn.classList.remove('playing');
                    utterance.onerror = () => btn.classList.remove('playing');
                }
                synth.speak(utterance);
            }

            function filterFAQs() {
                let filtered = faqData;
                if (activeCat !== 'all') {
                    filtered = filtered.filter(f => f.category === activeCat);
                }
                if (searchTerm.trim()) {
                    const term = searchTerm.trim().toLowerCase();
                    filtered = filtered.filter(f =>
                        f.question.toLowerCase().includes(term) ||
                        f.questionZh.includes(term) ||
                        f.answerEn.toLowerCase().includes(term) ||
                        f.answerZh.includes(term) ||
                        f.tags.some(t => t.toLowerCase().includes(term))
                    );
                }
                renderFAQs(filtered);
            }

            function renderFAQs(data) {
                faqCount.textContent = data.length;
                if (data.length === 0) {
                    faqList.innerHTML = `
                        <div class="empty-state">
                            <span class="icon">📭</span>
                            <p>没有找到匹配的问题</p>
                            <p style="font-size:12px;">请尝试其他关键词或筛选条件</p>
                        </div>`;
                    return;
                }
                let html = '';
                data.forEach((faq, idx) => {
                    html += `
                    <div class="faq-item" data-id="${faq.id}" data-cat="${faq.category}">
                        <div class="faq-question" onclick="toggleFAQ(this)">
                            <div class="q-icon">Q${idx + 1}</div>
                            <div class="q-content">
                                <div class="q-title">${faq.question}</div>
                                <span class="q-category ${faq.catClass}">${faq.categoryLabel}</span>
                            </div>
                            <span class="q-arrow">▼</span>
                        </div>
                        <div class="faq-answer">
                            <div class="answer-en">💬 ${faq.answerEn}</div>
                            <div class="answer-zh">📖 ${faq.answerZh}</div>
                            <div class="cultural-tip">
                                <span class="tip-icon">💡</span><b>Cultural Tip:</b> ${faq.culturalTip}
                            </div>
                            <button class="audio-btn" onclick="event.stopPropagation(); speakFAQ('${faq.answerEn.replace(/'/g, "\\'")}', this)">🔊 听英文回答</button>
                        </div>
                    </div>`;
                });
                faqList.innerHTML = html;
            }

            window.toggleFAQ = function(questionEl) {
                const item = questionEl.closest('.faq-item');
                if (!item) return;
                document.querySelectorAll('.faq-item.open').forEach(el => {
                    if (el !== item) el.classList.remove('open');
                });
                item.classList.toggle('open');
            };

            window.speakFAQ = function(text, btn) {
                speakTTS(text, btn);
            };

            searchInput.addEventListener('input', function() {
                searchTerm = this.value;
                filterFAQs();
            });

            document.querySelectorAll('#tagRow .filter-tag').forEach(tag => {
                tag.addEventListener('click', function() {
                    document.querySelectorAll('#tagRow .filter-tag').forEach(t => t.classList.remove('active'));
                    this.classList.add('active');
                    activeCat = this.dataset.cat;
                    filterFAQs();
                });
            });

            renderFAQs(faqData);
            faqCount.textContent = faqData.length;

            if ('speechSynthesis' in window) {
                window.speechSynthesis.getVoices();
            }
            console.log('🪶 国风华裳主题航班 · 旅客高频问答库已就绪');
            console.log('  共 ' + faqData.length + ' 个常见问题（含Cultural Tip）| 支持搜索筛选 | 点击展开查看标准回答');
        })();
    </script>
</body>
</html>
