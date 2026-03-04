import React, { useState, useEffect } from 'react';
import { BookOpen, FileText, CheckCircle, XCircle, ChevronLeft, ChevronRight, Home, BarChart2, Lightbulb, RefreshCw, Info } from 'lucide-react';

// --- 真實考古題庫與詳解 (採用台灣專業用語) ---
const ALL_QUESTIONS_POOL = [
  { 
    id: 1, 
    cat: "3.1 集排氣技術", 
    q: "在有害物質之發生處所，當其尚未擴散於作業場所之前，將其吸引排除之方式稱為？", 
    options: ["整體換氣", "局部排氣", "整體排氣", "自然通風"], 
    ans: 1,
    analysis: "正確答案是(2)局部排氣。這是工程控制中最有效的方法，在污染源擴散前就將其捕捉。 (1)整體換氣是用新鮮空氣稀釋濃度，效果較差；(3)(4)通常指自然或整廠通風，無法精準捕捉污染。"
  },
  { 
    id: 2, 
    cat: "3.1 集排氣技術", 
    q: "氣罩的型式很多，若依氣罩與污染源的相對位置分類，下列何者「有誤」？", 
    options: ["密閉式氣罩", "箱式氣罩", "外部氣罩", "電磁式氣罩"], 
    ans: 3,
    analysis: "正確答案是(4)。氣罩分類通常為：密閉式、箱式(包圍式)、外部式與接收式(或推拉式)。「電磁式」並非空氣污染集排氣技術中的氣罩分類。"
  },
  { 
    id: 3, 
    cat: "3.1 集排氣技術", 
    q: "對於有害物的作業場所，其工程控制或降低危害的集排氣系統中，「最優先」考慮的方法為？", 
    options: ["局部排氣裝置", "侷限裝置", "密閉設備", "整體換氣裝置"], 
    ans: 2,
    analysis: "正確答案是(3)密閉設備。根據工程控制階層，『源頭密閉』優於『局部排氣』，更優於『整體換氣』。只有在無法完全密閉時，才退而求其次選擇局部排氣。"
  },
  { 
    id: 12, 
    cat: "3.1 集排氣技術", 
    q: "局部排氣系統各單元設計的優先次序為何？ (a:風管; b:風車; c:氣罩)", 
    options: ["a、b、c", "c、b、a", "b、a、c", "c、a、b"], 
    ans: 3,
    analysis: "正確答案是(4)。設計順序必須從源頭開始：首先設計(c)氣罩決定捕捉風量，接著設計(a)風管計算阻力與流速，最後根據總流量與總壓損來選配(b)風車。"
  },
  { 
    id: 15, 
    cat: "3.1 集排氣技術", 
    q: "對一風車（風扇）而言，當轉速比改變時，其「馬力需求」與轉速比之關係為何？", 
    options: ["成正比", "與平方成正比", "與三次方成正比", "成反比"], 
    ans: 2,
    analysis: "正確答案是(3)。根據風車定律(Fans Law)：流量與轉速一次方成正比；靜壓與轉速平方成正比；『動力/馬力需求』則與轉速的三次方成正比。因此轉速增加 2 倍，馬力會增加 8 倍。"
  },
  { 
    id: 16, 
    cat: "3.1 集排氣技術", 
    q: "依靠吹氣與吸氣流的綜合作用來控制氣流擴散的氣罩稱為？", 
    options: ["下抽式氣罩", "推拉式氣罩", "側吸式氣罩", "狹縫式氣罩"], 
    ans: 1,
    analysis: "正確答案是(2)推拉式(Push-Pull)。利用吹氣將污染物推向吸氣口，可比單純外部氣罩節省風量且不易受橫向氣流干擾。其他選項僅有吸氣功能，無吹氣輔助。"
  },
  { 
    id: 33, 
    cat: "3.1 集排氣技術", 
    q: "對於圓形抽氣口，離其開口中心 1 倍口徑距離(X=D)處之風速，約會降為該抽氣口表面風速的幾分之幾？", 
    options: ["1/2", "1/20", "1/10", "1/4"], 
    ans: 2,
    analysis: "正確答案是(3)1/10。這是外部氣罩的特性，吸氣速度會隨著距離增加而迅速下降。在離門口一個直徑處，風速僅剩約 10%，這也是為什麼氣罩必須盡量靠近污染源的原因。"
  },
  { 
    id: 51, 
    cat: "3.2 採樣與檢測", 
    q: "為了判知樣品在「採樣過程」中是否遭受污染，應使用下列哪種空白樣品？", 
    options: ["運送空白", "現場空白", "方法空白", "設備空白"], 
    ans: 1,
    analysis: "正確答案是(2)現場空白。現場空白需在採樣地點打開瓶蓋模擬採樣過程，可檢測環境背景造成的污染。 (1)運送空白僅檢測運輸汙染；(3)方法空白檢測實驗室內污染；(4)設備空白檢測器材是否洗淨。"
  },
  { 
    id: 46, 
    cat: "3.2 採樣與檢測", 
    q: "等速吸引百分率（I%）用以判定是否維持等速速率採樣，其變化容許範圍為多少？", 
    options: ["±2%", "±5%", "±10%", "±15%"], 
    ans: 2,
    analysis: "正確答案是(3)±10%（即 90%~110%）。等速採樣是為了確保採得的粒狀物濃度具代表性。若偏差過大，會導致大顆粒粒徑分佈不均。 (2)±5% 通常是流量計校正的容許差。"
  },
  { 
    id: 49, 
    cat: "3.2 採樣與檢測", 
    q: "我國空氣品質標準中，細懸浮微粒（PM2.5）的 24 小時值標準值為？", 
    options: ["15 μg/m³", "25 μg/m³", "35 μg/m³", "50 μg/m³"], 
    ans: 2,
    analysis: "正確答案是(3) 35 μg/m³。這是台灣目前現行的空氣品質標準（2020年版）。 (1) 15 μg/m³ 是年平均值標準。"
  },
  { 
    id: 103, 
    cat: "3.3 操作維護", 
    q: "固定污染源設置操作許可證記載之各項許可條件數值，容許差值百分比為何？", 
    options: ["5%", "10%", "15%", "20%"], 
    ans: 1,
    analysis: "正確答案是(2) 10%。根據管理辦法，許可證登載之操作參數（如壓力、流量等）通常給予 10% 的彈性變動空間。若超過則可能涉及變更或違反操作。"
  },
  { 
    id: 104, 
    cat: "3.3 操作維護", 
    q: "倉庫入庫管理中，油品、藥劑及有保存期限之備品，應注意遵守何種原則？", 
    options: ["先進先出", "加權平均", "後進先出", "隨意選擇"], 
    ans: 0,
    analysis: "正確答案是(1)先進先出(FIFO)。這是管理消耗品的最基本原則，確保化學藥劑或濾袋不會因為存放過久而失效或劣化。"
  },
  { 
    id: 113, 
    cat: "3.3 操作維護", 
    q: "揮發性有機污染物（VOCs）控制設備中，活性碳吸附塔的入口廢氣濕度通常宜控制在？", 
    options: ["30%以下", "50%以下", "70%以下", "90%以下"], 
    ans: 1,
    analysis: "正確答案是(2) 50%以下。濕度過高時，水蒸氣會與污染物競爭活性碳上的吸附位點，大幅降低活性碳的吸附容量與處理效率。"
  },
  { 
    id: 121, 
    cat: "3.3 操作維護", 
    q: "活性碳吸附戴奧辛的效果，在廢氣溫度超過多少時會開始顯著下降？", 
    options: ["100°C", "120°C", "180°C", "250°C"], 
    ans: 2,
    analysis: "正確答案是(3) 180°C。活性碳吸附是物理作用，隨溫度升高而效果變差。在焚化爐控制中，噴粉活性碳通常要求在 150-180°C 以下操作以維持最佳效率。"
  },
  { 
    id: 125, 
    cat: "3.3 操作維護", 
    q: "下列何種保養策略屬於「時間基準維護（TBM）」？", 
    options: ["定期保養", "狀態基準維護", "事後維護", "預知保養"], 
    ans: 0,
    analysis: "正確答案是(1)定期保養。這類維護是根據時間週期（如每月、每季）進行更換或點檢。 (2)狀態基準維護是根據儀表顯示異常才維護；(3)事後維護則是壞了才修。"
  }
];

const App = () => {
  const [view, setView] = useState('home'); 
  const [examQuestions, setExamQuestions] = useState([]);
  const [currentIdx, setCurrentIdx] = useState(0);
  const [userAnswers, setUserAnswers] = useState({});
  const [isSubmitted, setIsSubmitted] = useState(false);

  // --- 初始化考試：從題庫中隨機挑選 15 題 ---
  const startExam = () => {
    const shuffled = [...ALL_QUESTIONS_POOL].sort(() => 0.5 - Math.random());
    setExamQuestions(shuffled.slice(0, 15));
    setUserAnswers({});
    setCurrentIdx(0);
    setIsSubmitted(false);
    setView('exam');
  };

  const handleAnswer = (idx) => {
    if (isSubmitted) return;
    setUserAnswers(prev => ({ ...prev, [currentIdx]: idx }));
  };

  const calculateScore = () => {
    let count = 0;
    examQuestions.forEach((q, i) => {
      if (userAnswers[i] === q.ans) count++;
    });
    return Math.round((count / examQuestions.length) * 100);
  };

  // --- 頁面：首頁 ---
  const HomeView = () => (
    <div className="flex flex-col items-center justify-center min-h-[80vh] p-6 text-center">
      <div className="bg-white p-10 rounded-[3rem] shadow-2xl border border-slate-100 max-w-2xl w-full">
        <div className="bg-blue-600 w-20 h-20 rounded-3xl flex items-center justify-center text-white mx-auto mb-6 shadow-xl shadow-blue-200">
          <BookOpen className="w-10 h-10" />
        </div>
        <h1 className="text-3xl font-black text-slate-800 mb-2">乙級空污技術員</h1>
        <p className="text-slate-500 font-bold mb-8 tracking-widest uppercase">考試準備 & 模擬考平台</p>
        
        <div className="space-y-4 mb-10">
          <div className="flex items-start gap-4 p-4 bg-slate-50 rounded-2xl text-left">
            <div className="bg-blue-100 p-2 rounded-lg text-blue-600 mt-1"><CheckCircle className="w-4 h-4"/></div>
            <div>
              <p className="font-bold text-slate-700">真實模擬環境</p>
              <p className="text-xs text-slate-500">每次隨機 15 題，模擬正式考試壓力</p>
            </div>
          </div>
          <div className="flex items-start gap-4 p-4 bg-slate-50 rounded-2xl text-left">
            <div className="bg-green-100 p-2 rounded-lg text-green-600 mt-1"><Info className="w-4 h-4"/></div>
            <div>
              <p className="font-bold text-slate-700">深度詳解解析</p>
              <p className="text-xs text-slate-500">不只給答案，更分析其餘選項錯誤原因</p>
            </div>
          </div>
        </div>

        <button 
          onClick={startExam}
          className="w-full py-5 bg-blue-600 text-white rounded-3xl font-black text-xl hover:bg-blue-700 transition-all shadow-2xl shadow-blue-100 active:scale-95"
        >
          開始模擬考
        </button>
      </div>
    </div>
  );

  // --- 頁面：測驗介面 ---
  const ExamView = () => {
    const q = examQuestions[currentIdx];
    if (!q) return null;

    return (
      <div className="max-w-2xl mx-auto p-6 pt-10">
        <div className="flex justify-between items-center mb-8">
          <span className="bg-slate-800 text-white px-4 py-1.5 rounded-2xl text-xs font-black tracking-widest">{q.cat}</span>
          <span className="text-slate-400 font-black text-sm uppercase">Quest. {currentIdx + 1} / 15</span>
        </div>

        <div className="bg-white rounded-[2.5rem] p-10 shadow-xl border border-slate-50 mb-8 min-h-[300px]">
          <h2 className="text-2xl font-bold text-slate-800 leading-snug mb-10">
            {q.q}
          </h2>
          <div className="space-y-4">
            {q.options.map((opt, i) => (
              <button
                key={i}
                onClick={() => handleAnswer(i)}
                className={`w-full text-left p-5 rounded-2xl border-2 transition-all flex items-center gap-5 ${
                  userAnswers[currentIdx] === i 
                    ? 'border-blue-500 bg-blue-50 text-blue-900' 
                    : 'border-slate-50 hover:border-slate-200 bg-slate-50 text-slate-600'
                }`}
              >
                <span className={`w-8 h-8 rounded-xl flex items-center justify-center font-black ${
                  userAnswers[currentIdx] === i ? 'bg-blue-600 text-white' : 'bg-white text-slate-300 border border-slate-100'
                }`}>
                  {String.fromCharCode(65 + i)}
                </span>
                <span className="font-bold text-lg">{opt}</span>
              </button>
            ))}
          </div>
        </div>

        <div className="flex justify-between items-center px-4">
          <button 
            disabled={currentIdx === 0}
            onClick={() => setCurrentIdx(currentIdx - 1)}
            className="flex items-center gap-2 font-black text-slate-400 disabled:opacity-30 p-2"
          >
            <ChevronLeft /> 上一題
          </button>
          
          {currentIdx === 14 ? (
            <button 
              onClick={() => { setIsSubmitted(true); setView('results'); }}
              className="px-12 py-4 bg-green-600 text-white rounded-3xl font-black shadow-xl hover:bg-green-700 active:scale-95 transition-all"
            >
              送出答案
            </button>
          ) : (
            <button 
              onClick={() => setCurrentIdx(currentIdx + 1)}
              className="flex items-center gap-2 font-black text-blue-600 p-2"
            >
              下一題 <ChevronRight />
            </button>
          )}
        </div>
      </div>
    );
  };

  // --- 頁面：結果與解析 ---
  const ResultView = () => {
    const score = calculateScore();
    return (
      <div className="max-w-3xl mx-auto p-6 py-12">
        <div className="bg-white rounded-[3rem] p-12 shadow-2xl text-center mb-12 border-b-[12px] border-blue-600">
          <h2 className="text-3xl font-black text-slate-800 mb-6 tracking-tight">測驗成績結算</h2>
          <div className="relative inline-flex items-center justify-center mb-8">
            <svg className="w-48 h-48 transform -rotate-90">
              <circle className="text-slate-100" strokeWidth="12" stroke="currentColor" fill="transparent" r="85" cx="96" cy="96" />
              <circle className="text-blue-600" strokeWidth="12" strokeDasharray={534} strokeDashoffset={534 - (534 * score) / 100} strokeLinecap="round" stroke="currentColor" fill="transparent" r="85" cx="96" cy="96" />
            </svg>
            <div className="absolute flex flex-col items-center">
              <span className="text-6xl font-black text-slate-800 tracking-tighter">{score}</span>
              <span className="text-xs font-black text-slate-400 uppercase tracking-widest">Points</span>
            </div>
          </div>
          <div className="flex gap-4 justify-center">
            <button onClick={startExam} className="px-10 py-4 bg-blue-600 text-white rounded-3xl font-black shadow-xl hover:scale-105 transition-transform">再次挑戰</button>
            <button onClick={() => setView('home')} className="px-10 py-4 bg-slate-100 text-slate-600 rounded-3xl font-black">返回首頁</button>
          </div>
        </div>

        <div className="space-y-8">
          <h3 className="text-2xl font-black text-slate-800 flex items-center gap-3 px-4">
            <BarChart2 className="w-8 h-8 text-blue-600" /> 詳解檢討區
          </h3>
          {examQuestions.map((q, i) => (
            <div key={i} className={`bg-white rounded-[2.5rem] p-8 shadow-sm border-l-[10px] ${userAnswers[i] === q.ans ? 'border-green-500' : 'border-red-500'}`}>
              <div className="flex items-center justify-between mb-4">
                <span className="text-xs font-black bg-slate-100 text-slate-500 px-3 py-1 rounded-full uppercase tracking-tighter">Question {i+1}</span>
                {userAnswers[i] === q.ans ? (
                  <span className="text-xs font-black text-green-600 flex items-center gap-1"><CheckCircle className="w-4 h-4"/> 回答正確</span>
                ) : (
                  <span className="text-xs font-black text-red-600 flex items-center gap-1"><XCircle className="w-4 h-4"/> 回答錯誤</span>
                )}
              </div>
              <p className="text-xl font-bold text-slate-800 mb-6 leading-relaxed">{q.q}</p>
              
              <div className="grid grid-cols-1 md:grid-cols-2 gap-3 mb-6">
                <div className={`p-4 rounded-2xl border ${userAnswers[i] === q.ans ? 'bg-green-50 border-green-100 text-green-800 font-bold' : 'bg-red-50 border-red-100 text-red-800'}`}>
                  你的選擇：{userAnswers[i] !== undefined ? String.fromCharCode(65 + userAnswers[i]) : "未作答"}
                </div>
                <div className="p-4 rounded-2xl border bg-blue-50 border-blue-100 text-blue-800 font-bold">
                  正確答案：{String.fromCharCode(65 + q.ans)}
                </div>
              </div>

              <div className="bg-slate-50 p-6 rounded-3xl">
                <div className="flex items-center gap-2 text-blue-600 mb-3">
                  <Lightbulb className="w-5 h-5" />
                  <span className="font-black text-sm uppercase tracking-widest">專業詳解分析</span>
                </div>
                <p className="text-slate-600 text-sm leading-relaxed font-medium">
                  {q.analysis}
                </p>
              </div>
            </div>
          ))}
        </div>
      </div>
    );
  };

  return (
    <div className="min-h-screen bg-slate-50 text-slate-900 font-sans selection:bg-blue-100">
      <nav className="bg-white/80 backdrop-blur-md sticky top-0 z-50 border-b border-slate-100 h-16 flex items-center px-6">
        <div className="max-w-5xl mx-auto w-full flex items-center justify-between">
          <div className="flex items-center gap-3 group cursor-pointer" onClick={() => setView('home')}>
            <div className="bg-blue-600 p-2 rounded-xl group-hover:rotate-12 transition-transform shadow-lg shadow-blue-100">
              <FileText className="text-white w-5 h-5" />
            </div>
            <span className="font-black text-xl text-slate-800 tracking-tighter">乙空模擬考 Pro</span>
          </div>
          <button onClick={startExam} className="bg-slate-900 text-white px-5 py-2 rounded-2xl text-xs font-black hover:bg-blue-600 transition-all active:scale-95">
            重新測驗
          </button>
        </div>
      </nav>

      <main className="pb-20">
        {view === 'home' && <HomeView />}
        {view === 'exam' && <ExamView />}
        {view === 'results' && <ResultView />}
      </main>

      <footer className="text-center text-slate-300 text-xs py-10 font-bold tracking-widest uppercase">
        © 2024 Air Pollution Control Specialist Preparation Platform
      </footer>
    </div>
  );
};

export default App;

