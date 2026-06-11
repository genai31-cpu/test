# test[광고문안생성기.html](https://github.com/user-attachments/files/28825840/default.html)
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI 광고 문안 생성기</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            color: white;
            margin-bottom: 40px;
        }

        .header h1 {
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 30px;
        }

        .input-section, .output-section {
            background: white;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
        }

        .section-title {
            font-size: 1.5em;
            color: #667eea;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 3px solid #667eea;
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            color: #333;
            font-weight: 600;
            font-size: 14px;
        }

        input[type="text"],
        textarea,
        select {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 14px;
            transition: all 0.3s;
            font-family: inherit;
        }

        input:focus,
        textarea:focus,
        select:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        textarea {
            resize: vertical;
            min-height: 80px;
        }

        .btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            width: 100%;
            margin-top: 10px;
            transition: transform 0.2s;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(102, 126, 234, 0.3);
        }

        .btn:active {
            transform: translateY(0);
        }

        .ad-card {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 12px;
            margin-bottom: 20px;
            border-left: 4px solid #667eea;
            position: relative;
            animation: slideIn 0.5s ease-out;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateX(-20px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .ad-card h3 {
            color: #667eea;
            margin-bottom: 10px;
            font-size: 1.1em;
        }

        .ad-text {
            color: #333;
            line-height: 1.6;
            margin-bottom: 15px;
            white-space: pre-wrap;
        }

        .ad-actions {
            display: flex;
            gap: 10px;
        }

        .btn-small {
            padding: 8px 16px;
            font-size: 14px;
            flex: 1;
            background: #28a745;
        }

        .btn-small.copy {
            background: #17a2b8;
        }

        .btn-small:hover {
            opacity: 0.9;
        }

        .style-selector {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 10px;
            margin-bottom: 20px;
        }

        .style-option {
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            cursor: pointer;
            text-align: center;
            transition: all 0.3s;
            background: white;
        }

        .style-option:hover {
            border-color: #667eea;
            background: #f8f9ff;
        }

        .style-option.active {
            border-color: #667eea;
            background: #667eea;
            color: white;
        }

        .style-option input[type="checkbox"] {
            margin-right: 5px;
        }

        .empty-state {
            text-align: center;
            padding: 60px 20px;
            color: #999;
        }

        .empty-state svg {
            width: 100px;
            height: 100px;
            margin-bottom: 20px;
            opacity: 0.3;
        }

        .loading {
            text-align: center;
            padding: 40px;
            color: #667eea;
        }

        .loading::after {
            content: '...';
            animation: dots 1.5s infinite;
        }

        @keyframes dots {
            0%, 20% { content: '.'; }
            40% { content: '..'; }
            60%, 100% { content: '...'; }
        }

        .char-count {
            text-align: right;
            font-size: 12px;
            color: #999;
            margin-top: 5px;
        }

        .tips {
            background: #fff3cd;
            padding: 15px;
            border-radius: 8px;
            margin-top: 20px;
            border-left: 4px solid #ffc107;
        }

        .tips h4 {
            color: #856404;
            margin-bottom: 10px;
        }

        .tips ul {
            margin-left: 20px;
            color: #856404;
        }

        .tips li {
            margin-bottom: 5px;
        }

        @media (max-width: 968px) {
            .main-content {
                grid-template-columns: 1fr;
            }

            .header h1 {
                font-size: 2em;
            }

            .style-selector {
                grid-template-columns: 1fr;
            }
        }

        .badge {
            display: inline-block;
            padding: 4px 8px;
            background: #667eea;
            color: white;
            border-radius: 4px;
            font-size: 12px;
            margin-left: 10px;
        }

        .example-btn {
            background: #6c757d;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🚀 AI 광고 문안 생성기</h1>
            <p>제품 정보를 입력하면 전문적인 광고 카피를 즉시 생성합니다</p>
        </div>

        <div class="main-content">
            <!-- 입력 섹션 -->
            <div class="input-section">
                <h2 class="section-title">📝 제품 정보 입력</h2>

                <form id="adForm">
                    <div class="form-group">
                        <label for="productName">제품명 *</label>
                        <input type="text" id="productName" required placeholder="예: 프리미엄 무선 이어폰">
                    </div>

                    <div class="form-group">
                        <label for="category">카테고리 *</label>
                        <select id="category" required>
                            <option value="">선택하세요</option>
                            <option value="전자제품">전자제품</option>
                            <option value="패션/뷰티">패션/뷰티</option>
                            <option value="식품/음료">식품/음료</option>
                            <option value="생활용품">생활용품</option>
                            <option value="건강/운동">건강/운동</option>
                            <option value="교육/서비스">교육/서비스</option>
                            <option value="기타">기타</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label for="features">주요 특징 (쉼표로 구분) *</label>
                        <textarea id="features" required placeholder="예: 노이즈 캔슬링, 30시간 재생, 방수 기능"></textarea>
                        <div class="char-count"><span id="featuresCount">0</span> 자</div>
                    </div>

                    <div class="form-group">
                        <label for="targetAudience">타겟 고객</label>
                        <input type="text" id="targetAudience" placeholder="예: 20-30대 직장인, 학생">
                    </div>

                    <div class="form-group">
                        <label for="price">가격 (선택)</label>
                        <input type="text" id="price" placeholder="예: 89,000원">
                    </div>

                    <div class="form-group">
                        <label for="promotion">프로모션/할인 정보</label>
                        <input type="text" id="promotion" placeholder="예: 50% 할인, 무료 배송">
                    </div>

                    <div class="form-group">
                        <label>광고 스타일 선택 (복수 선택 가능)</label>
                        <div class="style-selector">
                            <div class="style-option active" data-style="감성적">
                                <input type="checkbox" id="style1" value="감성적" checked>
                                <label for="style1">💝 감성적</label>
                            </div>
                            <div class="style-option" data-style="전문적">
                                <input type="checkbox" id="style2" value="전문적">
                                <label for="style2">💼 전문적</label>
                            </div>
                            <div class="style-option" data-style="유머러스">
                                <input type="checkbox" id="style3" value="유머러스">
                                <label for="style3">😄 유머러스</label>
                            </div>
                            <div class="style-option" data-style="긴급성">
                                <input type="checkbox" id="style4" value="긴급성">
                                <label for="style4">⚡ 긴급성</label>
                            </div>
                        </div>
                    </div>

                    <button type="submit" class="btn">✨ 광고 문안 생성하기</button>
                    <button type="button" class="btn example-btn" onclick="fillExample()">📋 예시 데이터 채우기</button>
                </form>

                <div class="tips">
                    <h4>💡 작성 팁</h4>
                    <ul>
                        <li>제품의 핵심 특징을 3-5개 입력하세요</li>
                        <li>타겟 고객을 명확히 하면 더 효과적입니다</li>
                        <li>프로모션 정보는 구체적으로 작성하세요</li>
                        <li>여러 스타일을 선택하면 다양한 문안을 받습니다</li>
                    </ul>
                </div>
            </div>

            <!-- 출력 섹션 -->
            <div class="output-section">
                <h2 class="section-title">🎯 생성된 광고 문안</h2>
                <div id="output">
                    <div class="empty-state">
                        <svg viewBox="0 0 24 24" fill="currentColor">
                            <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-5 14H7v-2h7v2zm3-4H7v-2h10v2zm0-4H7V7h10v2z"/>
                        </svg>
                        <p>왼쪽 폼을 작성하고<br>"광고 문안 생성하기"를 클릭하세요</p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 스타일 옵션 토글
        document.querySelectorAll('.style-option').forEach(option => {
            option.addEventListener('click', function() {
                const checkbox = this.querySelector('input[type="checkbox"]');
                checkbox.checked = !checkbox.checked;
                this.classList.toggle('active');
            });
        });

        // 글자 수 카운트
        document.getElementById('features').addEventListener('input', function() {
            document.getElementById('featuresCount').textContent = this.value.length;
        });

        // 예시 데이터 채우기
        function fillExample() {
            document.getElementById('productName').value = '프리미엄 무선 이어폰 AirPods Pro';
            document.getElementById('category').value = '전자제품';
            document.getElementById('features').value = '액티브 노이즈 캔슬링, 30시간 재생 시간, IPX7 방수, 초경량 디자인, 터치 컨트롤';
            document.getElementById('targetAudience').value = '20-30대 직장인, 음악 애호가';
            document.getElementById('price').value = '189,000원';
            document.getElementById('promotion').value = '출시 기념 30% 할인 + 무료 배송';
            document.getElementById('featuresCount').textContent = document.getElementById('features').value.length;
        }

        // 폼 제출
        document.getElementById('adForm').addEventListener('submit', function(e) {
            e.preventDefault();
            generateAds();
        });

        // 광고 문안 생성
        function generateAds() {
            const productName = document.getElementById('productName').value;
            const category = document.getElementById('category').value;
            const features = document.getElementById('features').value;
            const targetAudience = document.getElementById('targetAudience').value;
            const price = document.getElementById('price').value;
            const promotion = document.getElementById('promotion').value;

            const selectedStyles = Array.from(document.querySelectorAll('.style-option input:checked'))
                .map(input => input.value);

            if (selectedStyles.length === 0) {
                alert('최소 1개의 광고 스타일을 선택해주세요!');
                return;
            }

            // 로딩 표시
            document.getElementById('output').innerHTML = '<div class="loading">광고 문안을 생성하는 중입니다</div>';

            // 실제로는 여기서 AI API를 호출하겠지만, 템플릿 기반으로 생성
            setTimeout(() => {
                const ads = [];
                const featureList = features.split(',').map(f => f.trim());

                selectedStyles.forEach(style => {
                    ads.push(generateAdByStyle(style, {
                        productName,
                        category,
                        features: featureList,
                        targetAudience,
                        price,
                        promotion
                    }));
                });

                displayAds(ads);
            }, 1500);
        }

        // 스타일별 광고 생성
        function generateAdByStyle(style, data) {
            const templates = {
                '감성적': generateEmotionalAd(data),
                '전문적': generateProfessionalAd(data),
                '유머러스': generateHumorousAd(data),
                '긴급성': generateUrgentAd(data)
            };

            return {
                style: style,
                content: templates[style]
            };
        }

        function generateEmotionalAd(data) {
            const headlines = [
                `${data.productName}와 함께하는 특별한 순간`,
                `당신의 일상을 바꿀 ${data.productName}`,
                `${data.productName}로 시작하는 새로운 경험`
            ];

            const bodies = [
                `${data.targetAudience || '당신'}을 위한 완벽한 선택.\n${data.features.slice(0, 3).join(', ')}로 매일을 특별하게 만들어보세요.`,
                `소중한 순간을 더욱 의미있게.\n${data.productName}이 선사하는 프리미엄 경험을 느껴보세요.`,
                `일상의 작은 변화가 큰 행복을 만듭니다.\n${data.features[0]}부터 시작해보세요.`
            ];

            let ad = `${headlines[Math.floor(Math.random() * headlines.length)]}\n\n`;
            ad += `${bodies[Math.floor(Math.random() * bodies.length)]}\n\n`;
            
            if (data.promotion) {
                ad += `💝 특별 혜택: ${data.promotion}\n`;
            }
            if (data.price) {
                ad += `💰 ${data.price}\n`;
            }
            ad += `\n✨ 지금 바로 경험해보세요!`;

            return ad;
        }

        function generateProfessionalAd(data) {
            let ad = `${data.productName}\n`;
            ad += `${data.category} 분야의 혁신적인 솔루션\n\n`;
            ad += `주요 특징:\n`;
            data.features.forEach((feature, index) => {
                ad += `${index + 1}. ${feature}\n`;
            });
            ad += `\n`;
            
            if (data.targetAudience) {
                ad += `추천 대상: ${data.targetAudience}\n`;
            }
            if (data.price) {
                ad += `가격: ${data.price}\n`;
            }
            if (data.promotion) {
                ad += `\n🎁 프로모션: ${data.promotion}\n`;
            }
            ad += `\n전문가가 인정한 품질, 지금 확인하세요.`;

            return ad;
        }

        function generateHumorousAd(data) {
            const hooks = [
                `아직도 ${data.category} 고민 중이세요? 😅`,
                `${data.productName} 없이 어떻게 살았을까요? 🤔`,
                `친구들이 부러워할 준비 되셨나요? 😎`
            ];

            let ad = `${hooks[Math.floor(Math.random() * hooks.length)]}\n\n`;
            ad += `${data.productName}는 다릅니다!\n\n`;
            ad += `✅ ${data.features[0]}\n`;
            ad += `✅ ${data.features[1] || '놀라운 성능'}\n`;
            ad += `✅ ${data.features[2] || '합리적인 가격'}\n\n`;
            
            if (data.promotion) {
                ad += `🎉 ${data.promotion}\n`;
            }
            ad += `\n더 이상 고민하지 마세요! 😉`;

            return ad;
        }

        function generateUrgentAd(data) {
            let ad = `⚡ 긴급 공지 ⚡\n\n`;
            ad += `${data.productName}\n`;
            
            if (data.promotion) {
                ad += `${data.promotion}\n\n`;
                ad += `⏰ 이 기회를 놓치지 마세요!\n\n`;
            }
            
            ad += `핵심 스펙:\n`;
            data.features.slice(0, 3).forEach(feature => {
                ad += `🔥 ${feature}\n`;
            });
            
            if (data.price) {
                ad += `\n💰 특가: ${data.price}\n`;
            }
            
            ad += `\n⚠️ 한정 수량 / 조기 마감 가능\n`;
            ad += `👉 지금 바로 주문하세요!`;

            return ad;
        }

        // 광고 표시
        function displayAds(ads) {
            const output = document.getElementById('output');
            output.innerHTML = '';

            ads.forEach((ad, index) => {
                const card = document.createElement('div');
                card.className = 'ad-card';
                card.style.animationDelay = `${index * 0.1}s`;
                
                card.innerHTML = `
                    <h3>${getStyleIcon(ad.style)} ${ad.style} 스타일 <span class="badge">AI 생성</span></h3>
                    <div class="ad-text">${ad.content}</div>
                    <div class="ad-actions">
                        <button class="btn btn-small copy" onclick="copyAd(this, ${index})">📋 복사</button>
                        <button class="btn btn-small" onclick="downloadAd(${index})">💾 저장</button>
                    </div>
                `;
                
                output.appendChild(card);
            });
        }

        function getStyleIcon(style) {
            const icons = {
                '감성적': '💝',
                '전문적': '💼',
                '유머러스': '😄',
                '긴급성': '⚡'
            };
            return icons[style] || '📝';
        }

        // 광고 복사
        function copyAd(button, index) {
            const adText = document.querySelectorAll('.ad-text')[index].textContent;
            navigator.clipboard.writeText(adText).then(() => {
                const originalText = button.textContent;
                button.textContent = '✅ 복사됨!';
                button.style.background = '#28a745';
                setTimeout(() => {
                    button.textContent = originalText;
                    button.style.background = '';
                }, 2000);
            });
        }

        // 광고 다운로드
        function downloadAd(index) {
            const adText = document.querySelectorAll('.ad-text')[index].textContent;
            const style = document.querySelectorAll('.ad-card h3')[index].textContent;
            const blob = new Blob([`${style}\n\n${adText}`], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `광고문안_${index + 1}.txt`;
            a.click();
            URL.revokeObjectURL(url);
        }
    </script>
</body>
</html>
