<!-- Chosen Palette: Calm Harmony (Warm Neutrals + Professional Blue Accent) -->
<!-- Application Structure Plan: 대시보드 접근 방식을 채택했습니다. 상단 탐색 바(대시보드 요약, 상세 현황, 주요 리스크, 우선순위)를 통해 4개의 핵심 섹션 뷰(View)를 전환합니다. 이는 긴 스크롤 대신 사용자의 '작업'에 따라 정보를 그룹화하여 사용성을 극대화합니다 (예: '요약 파악', '상세 드릴다운', '리스크 인지', '조치 확인'). '상세 현황' 섹션 내에서는 프로젝트별 탭을 두어, 페이지 이동 없이도 특정 프로젝트의 세부 정보를(진행률/예산 도넛 차트, 이슈, 계획) 즉시 로드할 수 있게 하여 드릴다운을 용이하게 했습니다. -->
<!-- Visualization & Content Choices: [정보: 요약 KPI -> 목표: 전체 현황 비교 -> 방식: 레이더 차트 (Chart.js) -> 상호작용: 툴팁 -> 사유: 3개 프로젝트의 진행률/예산 집행률을 한눈에 비교하여 '프로필'을 파악하기 용이함.], [정보: 개별 프로젝트 진행/예산 -> 목표: 상세 상태 전달 -> 방식: 도넛 차트 2개 (Chart.js) -> 상호작용: 중앙 % 텍스트, 툴팁 -> 사유: 단순 숫자보다 시각적으로 즉각적인 상태 인지가 가능함.], [정보: 리스크 및 대응 -> 목표: 위험 강조 -> 방식: HTML/Tailwind 콜아웃 카드 (경고색 테두리) -> 상호작용: 없음 -> 사유: 테이블보다 시각적 경고 수준이 높음.], [정보: 우선순위 -> 목표: 실행 지시 -> 방식: 순위별 강조 카드 (HTML/Tailwind) -> 상호작용: 없음 -> 사유: 명확한 실행 순서 전달.] -->
<!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>주간 프로젝트 대시보드</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Noto Sans KR', sans-serif;
            background-color: #f8f9fa;
        }
        .section {
            display: none;
        }
        .section.active {
            display: block;
        }
        .nav-button {
            transition: all 0.3s ease;
            padding: 0.75rem 1rem;
            border-bottom: 3px solid transparent;
            font-weight: 500;
            color: #4b5563;
        }
        .nav-button:hover {
            color: #2563eb;
        }
        .nav-button.active {
            color: #2563eb;
            border-bottom-color: #2563eb;
        }
        .project-tab {
            transition: all 0.3s ease;
            padding: 0.5rem 1rem;
            border-bottom: 2px solid transparent;
            font-weight: 500;
            color: #6b7280;
        }
        .project-tab:hover {
            color: #3b82f6;
        }
        .project-tab.active {
            color: #3b82f6;
            border-bottom-color: #3b82f6;
        }
        .project-card {
            display: none;
        }
        .project-card.active {
            display: block;
        }
        .stat-card {
            background-color: white;
            border-radius: 0.5rem;
            box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
            padding: 1.5rem;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 500px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 350px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
        .donut-chart-container {
            position: relative;
            width: 100%;
            max-width: 180px;
            margin-left: auto;
            margin-right: auto;
            height: 180px;
            max-height: 180px;
        }
    </style>
</head>
<body class="text-neutral-800">

    <header class="bg-white shadow-sm">
        <div class="container mx-auto px-4 py-5 md:flex md:items-center md:justify-between">
            <h1 class="text-2xl font-bold text-blue-700">주간 프로젝트 대시보드</h1>
            <p class="text-neutral-500 font-medium mt-1 md:mt-0">2025년 10월 4주차</p>
        </div>
    </header>

    <nav class="bg-white shadow-sm sticky top-0 z-10">
        <div class="container mx-auto flex flex-wrap justify-center md:justify-start">
            <button class="nav-button active" data-section="summary">대시보드 요약</button>
            <button class="nav-button" data-section="details">프로젝트별 상세 현황</button>
            <button class="nav-button" data-section="risks">주요 리스크</button>
            <button class="nav-button" data-section="priorities">결론 및 우선순위</button>
        </div>
    </nav>

    <main class="container mx-auto px-4 py-8">

        <section id="summary-section" class="section active">
            <p class="text-lg text-neutral-700 mb-6">
                전체 프로젝트의 핵심 성과 지표(KPI)와 진행 현황을 요약합니다. 이 섹션에서는 평균 진행률, 예산 집행률 및 주요 이슈를 한눈에 파악할 수 있습니다.
            </p>
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-8">
                <div class="stat-card text-center">
                    <h3 class="text-sm font-medium text-neutral-500 uppercase">총 프로젝트</h3>
                    <p class="text-4xl font-bold text-blue-600 mt-2">3<span class="text-lg ml-1">건</span></p>
                </div>
                <div class="stat-card text-center">
                    <h3 class="text-sm font-medium text-neutral-500 uppercase">평균 진행률</h3>
                    <p class="text-4xl font-bold text-green-600 mt-2">63.3<span class="text-lg ml-1">%</span></p>
                </div>
                <div class="stat-card text-center">
                    <h3 class="text-sm font-medium text-neutral-500 uppercase">평균 예산 집행률</h3>
                    <p class="text-4xl font-bold text-orange-600 mt-2">58.3<span class="text-lg ml-1">%</span></p>
                </div>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <h2 class="text-xl font-bold text-center mb-4">프로젝트 현황 비교</h2>
                    <div class="chart-container">
                        <canvas id="projectRadarChart"></canvas>
                    </div>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md">
                    <h2 class="text-xl font-bold mb-4">주요 이슈 요약</h2>
                    <p class="text-neutral-700 leading-relaxed">
                        **외부 벤더 일정 지연** 및 **CEO 최종 승인 대기**로 인한 핵심 프로젝트 일정 리스크가 증대되고 있습니다. '신규 ERP' 건은 벤더 지연 및 범위 추가 리스크가 있으며, '브랜드 리뉴얼' 건은 핵심 경로(Critical Path) 상의 승인 지연이 문제입니다. '고객 데이터 분석' 1건은 최종 테스트 단계로 성공적인 완료가 임박했습니다.
                    </p>
                </div>
            </div>
        </section>

        <section id="details-section" class="section">
            <p class="text-lg text-neutral-700 mb-6">
                개별 프로젝트의 상세 현황을 확인합니다. 탭을 클릭하여 각 프로젝트의 진행률, 예산, 주요 이슈, 완료 작업 및 다음 주 계획을 드릴다운할 수 있습니다.
            </p>
            
            <div class="flex flex-wrap space-x-1 border-b border-neutral-200 mb-6">
                <button class="project-tab active" data-project="erp">신규 ERP 시스템 도입</button>
                <button class="project-tab" data-project="brand">2025 브랜드 리뉴얼</button>
                <button class="project-tab" data-project="data">고객 데이터 분석 시스템</button>
            </div>

            <div id="project-content-area">
                <div id="erp-content" class="project-card active bg-white p-6 rounded-lg shadow-md">
                    <h3 class="text-2xl font-bold text-blue-700">신규 ERP 시스템 도입</h3>
                    <p class="text-neutral-500 mb-4">IT운영팀 / 김철수 과장</p>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 my-4 text-center">
                        <div>
                            <h4 class="text-lg font-semibold mb-2">진행률</h4>
                            <div class="donut-chart-container">
                                <canvas id="erpProgressChart"></canvas>
                            </div>
                        </div>
                        <div>
                            <h4 class="text-lg font-semibold mb-2">예산 집행률</h4>
                            <div class="donut-chart-container">
                                <canvas id="erpBudgetChart"></canvas>
                            </div>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mt-6">
                        <div>
                            <h4 class="text-lg font-semibold text-red-600 mb-2">주요 이슈</h4>
                            <p class="text-neutral-700"><span class_D="text-lg mr-2">⚠️</span>**외부 벤더 일정 조율 지연 (3일)**</p>
                            <p class="text-neutral-700"><span class_D="text-lg mr-2">⚠️</span>회계팀 요구사항 **추가 접수** (Scope Risk)</p>
                        </div>
                        <div>
                            <h4 class="text-lg font-semibold text-green-600 mb-2">완료된 작업</h4>
                            <ul class="list-disc list-inside text-neutral-700 space-y-1">
                                <li>시스템 설계 완료</li>
                                <li>테스트 서버 구축 완료</li>
                            </ul>
                        </div>
                        <div>
                            <h4 class="text-lg font-semibold text-blue-600 mb-2">다음 주 계획</h4>
                            <ul class="list-disc list-inside text-neutral-700 space-y-1">
                                <li>회계 모듈 개발 착수</li>
                                <li>사용자 교육 자료 준비</li>
                            </ul>
                        </div>
                    </div>
                </div>

                <div id="brand-content" class="project-card bg-white p-6 rounded-lg shadow-md">
                    <h3 class="text-2xl font-bold text-blue-700">2025 브랜드 리뉴얼 캠페인</h3>
                    <p class="text-neutral-500 mb-4">마케팅팀 / 이영희 부장</p>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 my-4 text-center">
                        <div>
                            <h4 class="text-lg font-semibold mb-2">진행률</h4>
                            <div class="donut-chart-container">
                                <canvas id="brandProgressChart"></canvas>
                            </div>
                        </div>
                        <div>
                            <h4 class="text-lg font-semibold mb-2">예산 집행률</h4>
                            <div class="donut-chart-container">
                                <canvas id="brandBudgetChart"></canvas>
                            </div>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mt-6">
                        <div>
                            <h4 class="text-lg font-semibold text-red-600 mb-2">주요 이슈</h4>
                            <p class="text-neutral-700"><span class_D="text-lg mr-2">⚠️</span>**CEO 최종 승인 대기 중 (Critical Path 지연)**</p>
                        </div>
                        <div>
                            <h4 class="text-lg font-semibold text-green-600 mb-2">완료된 작업</h4>
                            <ul class="list-disc list-inside text-neutral-700 space-y-1">
                                <li>시장 조사 및 컨셉 개발</li>
                                <li>디자인 시안 3종 개발</li>
                            </ul>
                        </div>
                        <div>
                            <h4 class="text-lg font-semibold text-blue-600 mb-2">다음 주 계획</h4>
                            <ul class="list-disc list-inside text-neutral-700 space-y-1">
                                <li>최종 디자인 확정</li>
                                <li>제작업체 선정</li>
                            </ul>
                        </div>
                    </div>
                </div>

                <div id="data-content" class="project-card bg-white p-6 rounded-lg shadow-md">
                    <h3 class="text-2xl font-bold text-blue-700">고객 데이터 분석 시스템 구축</h3>
                    <p class="text-neutral-500 mb-4">데이터분석팀 / 박민수 차장</p>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 my-4 text-center">
                        <div>
                            <h4 class="text-lg font-semibold mb-2">진행률</h4>
                            <div class="donut-chart-container">
                                <canvas id="dataProgressChart"></canvas>
                            </div>
                        </div>
                        <div>
                            <h4 class="text-lg font-semibold mb-2">예산 집행률</h4>
                            <div class="donut-chart-container">
                                <canvas id="dataBudgetChart"></canvas>
                            </div>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mt-6">
                        <div>
                            <h4 class="text-lg font-semibold text-green-600 mb-2">주요 이슈</h4>
                            <p class="text-neutral-700"><span class="text-lg mr-2">✅</span>**최종 테스트 단계 (점검 완료 임박)**</p>
                            <p class="text-neutral-700"><span class="text-lg mr-2">✅</span>개인정보보호 검토 완료</p>
                        </div>
                        <div>
                            <h4 class="text-lg font-semibold text-green-600 mb-2">완료된 작업</h4>
                            <ul class="list-disc list-inside text-neutral-700 space-y-1">
                                <li>데이터 파이프라인 개발</li>
                                <li>대시보드 개발</li>
                                <li>내부 테스트 완료</li>
                            </ul>
                        </div>
                        <div>
                            <h4 class="text-lg font-semibold text-blue-600 mb-2">다음 주 계획</h4>
                            <ul class="list-disc list-inside text-neutral-700 space-y-1">
                                <li>최종 사용자 테스트 (UAT)</li>
                                <li>운영 매뉴얼 배포</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section id="risks-section" class="section">
            <p class="text-lg text-neutral-700 mb-6">
                현재 프로젝트 진행에 영향을 미치는 공통적인 핵심 리스크와 구체적인 대응 방안을 설명합니다. 이는 선제적인 문제 해결을 위한 관리 포인트를 제공합니다.
            </p>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="bg-white p-6 rounded-lg shadow-md border-l-4 border-red-500">
                    <h3 class="text-xl font-bold text-red-700 mb-3">외부 협력사 일정 통제 미흡</h3>
                    <p class="text-neutral-700 font-medium mb-2">'신규 ERP 시스템 도입' 건에서 외부 벤더의 일정 조율 지연이 발생했으며, 이는 전체 일정 Risk로 확대될 가능성이 있습니다.</p>
                    <hr class="my-4">
                    <h4 class="text-lg font-semibold text-neutral-800 mb-2">대응 방안 (Mitigation)</h4>
                    <p class="text-neutral-700">**벤더사 관리 방안을 재수립하고 패널티 조항을 검토합니다.** 주간 단위 진척 보고를 의무화하고 IT운영팀 책임자가 직접 관여를 강화합니다.</p>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md border-l-4 border-yellow-500">
                    <h3 class="text-xl font-bold text-yellow-700 mb-3">상위 의사결정 지연</h3>
                    <p class="text-neutral-700 font-medium mb-2">'브랜드 리뉴얼 캠페인'의 최종 디자인 승인이 지연되고 있습니다. 이는 후속 제작 일정 전체를 지연시키는 Critical Path Risk입니다.</p>
                    <hr class="my-4">
                    <h4 class="text-lg font-semibold text-neutral-800 mb-2">대응 방안 (Mitigation)</h4>
                    <p class="text-neutral-700">CEO 비서실을 통해 **긴급 일정을 확보하도록 요청합니다.** 승인 즉시 제작업체 선정을 병행 착수하는 Fast-Track 전략을 준비합니다.</p>
                </div>
            </div>
        </section>
        
        <section id="priorities-section" class="section">
            <p class="text-lg text-neutral-700 mb-6">
                분석 결과를 바탕으로, 다음 주 경영진이 우선적으로 관리해야 할 프로젝트를 1순위부터 3순위까지 추천합니다. 이는 리스크가 크거나 즉각적인 조치가 필요한 순서입니다.
            </p>

            <div class="space-y-4">
                <div class="bg-white p-6 rounded-lg shadow-md border-l-4 border-red-600">
                    <div class="flex items-center">
                        <span class="text-3xl font-bold text-red-600 mr-5">1순위</span>
                        <div class="flex-1">
                            <h3 class="text-xl font-bold text-neutral-800">신규 ERP 시스템 도입</h3>
                            <p class="text-neutral-600 mt-1">외부 벤더 일정 지연 및 회계팀 요구사항 추가로 **일정 및 범위(Scope) Risk가 동시에 발생**했습니다. 즉각적인 Risk 대응 및 통제가 요구됩니다.</p>
                        </div>
                    </div>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md border-l-4 border-yellow-600">
                    <div class="flex items-center">
                        <span class="text-3xl font-bold text-yellow-600 mr-5">2순위</span>
                        <div class="flex-1">
                            <h3 class="text-xl font-bold text-neutral-800">2025 브랜드 리뉴얼 캠페인</h3>
                            <p class="text-neutral-600 mt-1">Critical Path 상의 CEO 승인이 대기 중입니다. **의사결정 지연이 전체 캠페인 일정에 치명적**이므로, 승인 일정 확보가 최우선 과제입니다.</p>
                        </div>
                    </div>
                </div>
                <div class="bg-white p-6 rounded-lg shadow-md border-l-4 border-blue-600">
                    <div class="flex items-center">
                        <span class="text-3xl font-bold text-blue-600 mr-5">3순위</span>
                        <div class="flex-1">
                            <h3 class="text-xl font-bold text-neutral-800">고객 데이터 분석 시스템 구축</h3>
                            <p class="text-neutral-600 mt-1">최종 UAT 단계를 앞두고 있습니다. **성공적인 마무리를 위한 안정성 및 사용자 전환 준비**에 대한 세밀한 점검이 필요합니다.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <footer class="text-center py-6 mt-8 border-t border-neutral-200">
        <p class="text-sm text-neutral-500">인터랙티브 프로젝트 대시보드 | 자동 생성됨</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', () => {

            const projectData = {
                erp: { name: '신규 ERP', progress: 65, budget: 58 },
                brand: { name: '브랜드 리뉴얼', progress: 40, budget: 35 },
                data: { name: '데이터 분석', progress: 85, budget: 82 }
            };

            const donutCenterTextPlugin = {
                id: 'centerText',
                afterDraw(chart) {
                    if (chart.config.type !== 'doughnut') return;
                    const ctx = chart.ctx;
                    const { width, height } = chart.chartArea;
                    ctx.save();
                    const dataPoint = chart.data.datasets[0].data[0];
                    const text = `${dataPoint}%`;
                    
                    ctx.font = `bold ${width / 5}px "Noto Sans KR"`;
                    ctx.textAlign = 'center';
                    ctx.textBaseline = 'middle';
                    const color = chart.data.datasets[0].backgroundColor[0] || '#000';
                    ctx.fillStyle = color;
                    
                    ctx.fillText(text, width / 2, height / 2 + (height * 0.05));
                    ctx.restore();
                }
            };
            
            Chart.register(donutCenterTextPlugin);

            function createRadarChart() {
                const ctx = document.getElementById('projectRadarChart');
                if (!ctx) return;
                new Chart(ctx, {
                    type: 'radar',
                    data: {
                        labels: [projectData.erp.name, projectData.brand.name, projectData.data.name],
                        datasets: [
                            {
                                label: '진행률 (%)',
                                data: [projectData.erp.progress, projectData.brand.progress, projectData.data.progress],
                                backgroundColor: 'rgba(59, 130, 246, 0.2)',
                                borderColor: 'rgba(59, 130, 246, 1)',
                                borderWidth: 2,
                                pointBackgroundColor: 'rgba(59, 130, 246, 1)',
                            },
                            {
                                label: '예산 집행률 (%)',
                                data: [projectData.erp.budget, projectData.brand.budget, projectData.data.budget],
                                backgroundColor: 'rgba(249, 115, 22, 0.2)',
                                borderColor: 'rgba(249, 115, 22, 1)',
                                borderWidth: 2,
                                pointBackgroundColor: 'rgba(249, 115, 22, 1)',
                            }
                        ]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: {
                            r: {
                                beginAtZero: true,
                                max: 100,
                                ticks: {
                                    stepSize: 20
                                }
                            }
                        },
                        plugins: {
                            tooltip: {
                                callbacks: {
                                    label: function(context) {
                                        return `${context.dataset.label}: ${context.raw}%`;
                                    }
                                }
                            }
                        }
                    }
                });
            }

            function createDonutChart(canvasId, percentage, color) {
                const ctx = document.getElementById(canvasId);
                if (!ctx) return;
                new Chart(ctx, {
                    type: 'doughnut',
                    data: {
                        datasets: [{
                            data: [percentage, 100 - percentage],
                            backgroundColor: [color, '#e5e7eb'],
                            borderColor: ['#ffffff', '#ffffff'],
                            borderWidth: 2,
                            hoverOffset: 4
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        cutout: '70%',
                        plugins: {
                            legend: {
                                display: false
                            },
                            tooltip: {
                                enabled: false
                            }
                        }
                    }
                });
            }

            function initNav() {
                const navButtons = document.querySelectorAll('.nav-button');
                const sections = document.querySelectorAll('.section');

                navButtons.forEach(button => {
                    button.addEventListener('click', () => {
                        const sectionId = button.getAttribute('data-section');
                        
                        navButtons.forEach(btn => btn.classList.remove('active'));
                        button.classList.add('active');
                        
                        sections.forEach(section => {
                            if (section.id === `${sectionId}-section`) {
                                section.classList.add('active');
                            } else {
                                section.classList.remove('active');
                            }
                        });
                    });
                });
            }

            function initProjectTabs() {
                const projectTabs = document.querySelectorAll('.project-tab');
                const projectContents = document.querySelectorAll('.project-card');

                projectTabs.forEach(tab => {
                    tab.addEventListener('click', () => {
                        const projectId = tab.getAttribute('data-project');
                        
                        projectTabs.forEach(t => t.classList.remove('active'));
                        tab.classList.add('active');
                        
                        projectContents.forEach(content => {
                            if (content.id === `${projectId}-content`) {
                                content.classList.add('active');
                            } else {
                                content.classList.remove('active');
                            }
                        });
                    });
                });
            }

            createRadarChart();
            
            createDonutChart('erpProgressChart', projectData.erp.progress, '#22c55e');
            createDonutChart('erpBudgetChart', projectData.erp.budget, '#f97316');
            
            createDonutChart('brandProgressChart', projectData.brand.progress, '#22c55e');
            createDonutChart('brandBudgetChart', projectData.brand.budget, '#f97316');
            
            createDonutChart('dataProgressChart', projectData.data.progress, '#22c55e');
            createDonutChart('dataBudgetChart', projectData.data.budget, '#f97316');

            initNav();
            initProjectTabs();
        });
    </script>
</body>
</html>