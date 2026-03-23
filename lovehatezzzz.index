import React, { useState, useRef, useEffect } from 'react';

// === API Configuration ===
// The execution environment provides the key at runtime. 
const apiKey = ""; 

export default function App() {
  const [currentView, setCurrentView] = useState('intro'); // intro, capture, loading, result
  const [imageSrc, setImageSrc] = useState(null);
  const [analysisResult, setAnalysisResult] = useState(null);

  const navigateTo = (view) => setCurrentView(view);

  return (
    <div className="min-h-screen bg-[#1a1520] text-gray-100 font-sans selection:bg-[#ff477e]/50 relative overflow-hidden">
      {/* Global styles for Pixel Art Theme & Fonts */}
      <style dangerouslySetInnerHTML={{__html: `
        @import url('https://fonts.googleapis.com/css2?family=DotGothic16&display=swap');
        
        .pixel-font {
          font-family: 'DotGothic16', monospace;
          letter-spacing: 1px;
        }
        
        .pixel-box {
          background-color: #2b2235;
          border: 4px solid #000;
          box-shadow: 6px 6px 0px 0px #000;
        }

        .pixel-btn-love {
          background-color: #ff477e;
          border: 4px solid #000;
          box-shadow: 4px 4px 0px 0px #000;
          transition: transform 0.1s, box-shadow 0.1s;
        }
        .pixel-btn-love:active {
          transform: translate(4px, 4px);
          box-shadow: 0px 0px 0px 0px #000;
        }

        .pixel-btn-hate {
          background-color: #ff3838;
          border: 4px solid #000;
          box-shadow: 4px 4px 0px 0px #000;
          transition: transform 0.1s, box-shadow 0.1s;
        }
        .pixel-btn-hate:active {
          transform: translate(4px, 4px);
          box-shadow: 0px 0px 0px 0px #000;
        }

        .pixel-btn-neutral {
          background-color: #4b6584;
          border: 4px solid #000;
          box-shadow: 4px 4px 0px 0px #000;
          transition: transform 0.1s, box-shadow 0.1s;
        }
        .pixel-btn-neutral:active {
          transform: translate(4px, 4px);
          box-shadow: 0px 0px 0px 0px #000;
        }

        /* Blocky Scanline Animation */
        @keyframes blockyScan {
          0% { top: 0%; height: 10px; opacity: 0.8; }
          50% { height: 20px; opacity: 1; }
          100% { top: 100%; height: 10px; opacity: 0.8; }
        }
        .animate-pixel-scan {
          animation: blockyScan 2s steps(20) infinite;
        }

        /* CRT Overlay */
        .crt-overlay {
          background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
          background-size: 100% 4px, 6px 100%;
          pointer-events: none;
        }
      `}} />

      {/* Decorative Background Grid */}
      <div className="absolute inset-0 bg-[linear-gradient(rgba(255,255,255,0.03)_2px,transparent_2px),linear-gradient(90deg,rgba(255,255,255,0.03)_2px,transparent_2px)] bg-[size:32px_32px] pointer-events-none"></div>

      <main className="max-w-2xl mx-auto p-4 md:p-8 h-full min-h-screen flex flex-col justify-center relative z-10 pixel-font">
        {currentView === 'intro' && <IntroView onStart={() => navigateTo('capture')} />}
        {currentView === 'capture' && (
          <CaptureView 
            onCapture={(img) => {
              setImageSrc(img);
              navigateTo('loading');
            }} 
            onBack={() => navigateTo('intro')} 
          />
        )}
        {currentView === 'loading' && <LoadingView imageSrc={imageSrc} onComplete={(result) => {
          setAnalysisResult(result);
          navigateTo('result');
        }} />}
        {currentView === 'result' && (
          <ResultView 
            imageSrc={imageSrc} 
            result={analysisResult} 
            onRetry={() => {
              setImageSrc(null);
              setAnalysisResult(null);
              navigateTo('intro');
            }} 
          />
        )}
      </main>
    </div>
  );
}

// ==========================================
// 1. Intro View (首頁)
// ==========================================
function IntroView({ onStart }) {
  return (
    <div className="flex flex-col items-center justify-center text-center space-y-10 animate-in fade-in zoom-in duration-300">
      <div className="pixel-box p-8 w-full max-w-md relative bg-[#2d2438]">
        {/* Decorative Love/Hate Corner Pixels */}
        <div className="absolute -top-4 -left-4 text-4xl transform -rotate-12">💖</div>
        <div className="absolute -bottom-4 -right-4 text-4xl transform rotate-12">💢</div>

        <div className="text-5xl mb-4 tracking-widest">VS</div>
        <h1 className="text-3xl md:text-4xl font-black mb-4 leading-tight text-white drop-shadow-[2px_2px_0_#ff3838]">
          另一半怒氣<br/><span className="text-[#ff477e]">分析儀</span>
        </h1>
        <p className="text-[#a5b1c2] text-sm uppercase tracking-widest border-t-2 border-dashed border-[#4b6584] pt-4">
          LOVE & HATE SYSTEM V1.0
        </p>
      </div>

      <div className="pixel-box p-6 max-w-md w-full text-left bg-[#1e272e]">
        <p className="text-[#d2dae2] leading-8 text-sm md:text-base">
          <span className="text-[#ff477e] font-bold bg-[#ff477e]/20 px-1">【系統警告】</span> <br/>
          請在雷達偵測到高能反應前，預測目標的怒氣值！<br/>
          這是一款攸關生死存亡的像素級 AI 掃描工具。<br/>
          <span className="text-[#ff3838] mt-2 block">▶ 準備好面對現實了嗎？</span>
        </p>
      </div>

      <button 
        onClick={onStart}
        className="pixel-btn-love text-white px-10 py-5 text-xl font-bold flex items-center gap-3 w-full max-w-sm justify-center"
      >
        <span className="text-2xl">⚡</span> 啟動掃描程序
      </button>
    </div>
  );
}

// ==========================================
// 2. Capture View (拍照/上傳頁面)
// ==========================================
function CaptureView({ onCapture, onBack }) {
  const videoRef = useRef(null);
  const canvasRef = useRef(null);
  const fileInputRef = useRef(null);
  const [stream, setStream] = useState(null);
  const [cameraError, setCameraError] = useState('');

  useEffect(() => {
    let activeStream = null;
    const startCamera = async () => {
      try {
        const mediaStream = await navigator.mediaDevices.getUserMedia({ 
          video: { facingMode: 'user' } 
        });
        if (videoRef.current) {
          videoRef.current.srcObject = mediaStream;
        }
        setStream(mediaStream);
        activeStream = mediaStream;
      } catch (err) {
        setCameraError('相機連線失敗 [ERROR_NO_CAM]');
      }
    };
    startCamera();
    return () => {
      if (activeStream) activeStream.getTracks().forEach(track => track.stop());
    };
  }, []);

  const handleCapture = () => {
    if (videoRef.current && canvasRef.current) {
      const video = videoRef.current;
      const canvas = canvasRef.current;
      canvas.width = video.videoWidth;
      canvas.height = video.videoHeight;
      const ctx = canvas.getContext('2d');
      ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
      onCapture(canvas.toDataURL('image/jpeg', 0.8));
    }
  };

  const handleFileUpload = (e) => {
    const file = e.target.files[0];
    if (file) {
      const reader = new FileReader();
      reader.onloadend = () => onCapture(reader.result);
      reader.readAsDataURL(file);
    }
  };

  return (
    <div className="flex flex-col h-full animate-in fade-in duration-300">
      <div className="flex items-center mb-6 border-b-4 border-black pb-4 bg-[#1a1520] sticky top-0 z-20">
        <button onClick={onBack} className="pixel-btn-neutral px-4 py-2 text-white mr-4">
          ⬅️ BACK
        </button>
        <h2 className="text-2xl font-bold text-[#ff477e] drop-shadow-[2px_2px_0_#000]">目標鎖定</h2>
      </div>

      <div className="flex-1 flex flex-col items-center justify-center pixel-box p-6">
        
        {cameraError ? (
          <div className="text-center p-8 bg-black border-4 border-[#ff3838] w-full max-w-sm">
            <div className="text-5xl mb-4">💀</div>
            <p className="text-[#ff3838]">{cameraError}</p>
          </div>
        ) : (
          <div className="relative w-full max-w-sm bg-black aspect-[3/4] border-4 border-black shadow-[inset_0_0_20px_rgba(0,0,0,1)] flex items-center justify-center overflow-hidden">
            <div className="absolute inset-0 crt-overlay z-10"></div>
            <video 
              ref={videoRef} 
              autoPlay 
              playsInline 
              muted 
              className="absolute inset-0 w-full h-full object-cover transform scale-x-[-1] filter contrast-125 saturate-150" 
            />
            {/* Viewfinder Overlay */}
            <div className="absolute inset-0 z-20 pointer-events-none p-4 flex flex-col justify-between">
               <div className="flex justify-between">
                 <div className="w-8 h-8 border-t-4 border-l-4 border-[#ff477e]"></div>
                 <div className="w-8 h-8 border-t-4 border-r-4 border-[#ff477e]"></div>
               </div>
               <div className="flex justify-center items-center h-full opacity-50 text-[#ff477e]">
                  [ REC ]
               </div>
               <div className="flex justify-between">
                 <div className="w-8 h-8 border-b-4 border-l-4 border-[#ff477e]"></div>
                 <div className="w-8 h-8 border-b-4 border-r-4 border-[#ff477e]"></div>
               </div>
            </div>
          </div>
        )}
        <canvas ref={canvasRef} className="hidden" />

        <div className="mt-8 flex flex-col sm:flex-row gap-4 w-full max-w-sm">
          <button 
            onClick={handleCapture}
            disabled={!!cameraError || !stream}
            className="flex-1 pixel-btn-hate text-white py-4 px-4 font-bold disabled:opacity-50 disabled:cursor-not-allowed flex items-center justify-center gap-2"
          >
            📸 拍照分析
          </button>
          
          <button 
            onClick={() => fileInputRef.current?.click()}
            className="flex-1 pixel-btn-neutral text-white py-4 px-4 font-bold flex items-center justify-center gap-2"
          >
            📁 載入檔案
          </button>
          <input type="file" ref={fileInputRef} onChange={handleFileUpload} accept="image/*" className="hidden" />
        </div>
      </div>
    </div>
  );
}

// ==========================================
// 3. Loading View (分析載入中)
// ==========================================
function LoadingView({ imageSrc, onComplete }) {
  useEffect(() => {
    const performAnalysis = async () => {
      const base64Data = imageSrc.split(',')[1];
      const mimeType = imageSrc.split(';')[0].split(':')[1];

      const promptText = `你是一個專業的面部表情與心理學分析專家。請仔細分析這張照片中人物的面部表情，判斷其「怒氣指數」與脾氣狀態。
請務必以 JSON 格式回傳，且只能輸出 JSON，格式如下：
{
  "pointers": [
    {"feature": "眉毛", "analysis": "詳細的微表情分析結果..."},
    {"feature": "眼睛", "analysis": "詳細的微表情分析結果..."},
    {"feature": "嘴巴", "analysis": "詳細的微表情分析結果..."}
  ],
  "overallScore": 85, // 0 到 100 之間的整數，代表怒氣指數
  "overallComment": "對目前狀態的整體幽默評價...",
  "recommendation": "給使用者的搞笑求生建議..."
}
請使用繁體中文 (Traditional Chinese) 回答，語氣可以帶點幽默、強烈的求生欲，甚至帶點復古RPG遊戲的口吻（如 HP、魔王、戰鬥力）。
如果照片中沒有清楚的人臉，請假裝有偵測到不明魔物能量，並隨機給出一個搞笑的極端數值與建議。`;

      const payload = {
        contents: [{ role: "user", parts: [ { text: promptText }, { inlineData: { mimeType: mimeType || "image/jpeg", data: base64Data } } ] }],
        generationConfig: { responseMimeType: "application/json" }
      };

      const getMockResult = () => ({
        pointers: [
          { feature: "裝甲(眉頭)", analysis: "眉頭深鎖呈現倒八字型，防禦力極高，顯示極度不耐煩。" },
          { feature: "雷射(眼神)", analysis: "目光銳利帶有強烈殺氣，瞳孔微縮，建議裝備反光盾以免被秒殺。" },
          { feature: "火炮(嘴角)", analysis: "肌肉緊繃，這是在用力壓抑即將脫口而出的破壞性魔法詠唱。" }
        ],
        overallScore: Math.floor(Math.random() * 40) + 60,
        overallComment: "狀態：【最終 BOSS 覺醒前夕】。周圍氣壓極低，隨時可能進入狂暴狀態。",
        recommendation: "強烈建議立即存檔！主動奉上回血道具（珍奶或甜點），並選擇 [下跪道歉] 指令！"
      });

      let retries = 0;
      const delays = [1000, 2000, 4000, 8000];

      while (retries < 5) {
        try {
          if (!apiKey) throw new Error("No API key");
          const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
            method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify(payload)
          });
          if (!response.ok) throw new Error('API Request Failed');
          const data = await response.json();
          const textResponse = data.candidates?.[0]?.content?.parts?.[0]?.text;
          if (textResponse) {
            onComplete(JSON.parse(textResponse));
            return;
          } else throw new Error("Invalid format");
        } catch (error) {
          if (retries === 4 || !apiKey) {
            setTimeout(() => onComplete(getMockResult()), 2500);
            return;
          }
          await new Promise(r => setTimeout(r, delays[retries]));
          retries++;
        }
      }
    };
    performAnalysis();
  }, [imageSrc, onComplete]);

  return (
    <div className="flex flex-col items-center justify-center text-center space-y-8 h-full bg-[#1a1520] crt-overlay">
      <h2 className="text-3xl font-bold text-[#ff3838] animate-pulse drop-shadow-[2px_2px_0_#000]">PROCESSING...</h2>
      
      <div className="relative w-64 h-64 border-8 border-black shadow-[8px_8px_0_0_#000] bg-black">
        <img src={imageSrc} alt="Analyzing" className="w-full h-full object-cover filter contrast-150 grayscale-[50%] brightness-75 pixelated" />
        
        {/* Pixel Grid Overlay */}
        <div className="absolute inset-0 bg-[linear-gradient(rgba(0,0,0,0.5)_2px,transparent_2px),linear-gradient(90deg,rgba(0,0,0,0.5)_2px,transparent_2px)] bg-[size:8px_8px] pointer-events-none"></div>
        
        {/* Blocky Scanline */}
        <div className="absolute left-0 right-0 bg-[#ff3838] animate-pixel-scan shadow-[0_0_15px_#ff3838]"></div>
      </div>

      <div className="space-y-4 w-64 text-left">
        <div className="flex items-center gap-2">
           <span className="text-[#ff477e]">▶</span> <span className="text-white">EXTRACTING PIXELS</span>
        </div>
        <div className="flex items-center gap-2">
           <span className="text-[#ff477e]">▶</span> <span className="text-white">CALCULATING HATE_LVL</span>
        </div>
        <div className="flex items-center gap-2">
           <span className="text-[#ff477e] animate-pulse">▶</span> <span className="text-white animate-pulse">EVALUATING SURVIVAL...</span>
        </div>
        
        {/* Retro Progress Bar */}
        <div className="w-full h-6 border-4 border-white p-1 mt-4 flex">
          <div className="h-full bg-[#ff3838] w-[70%] animate-pulse"></div>
        </div>
      </div>
    </div>
  );
}

// ==========================================
// 4. Result View (結果頁面)
// ==========================================
function ResultView({ imageSrc, result, onRetry }) {
  if (!result) return null;

  const getThemeVars = (score) => {
    if (score < 40) return { 
      color: 'text-[#2ed573]', 
      bg: 'bg-[#2ed573]', 
      border: 'border-[#2ed573]',
      icon: '💖', 
      title: 'SAFE ZONE' 
    };
    if (score < 70) return { 
      color: 'text-[#ffa502]', 
      bg: 'bg-[#ffa502]', 
      border: 'border-[#ffa502]',
      icon: '⚠️', 
      title: 'WARNING' 
    };
    return { 
      color: 'text-[#ff4757]', 
      bg: 'bg-[#ff4757]', 
      border: 'border-[#ff4757]',
      icon: '💀', 
      title: 'DANGER!' 
    };
  };

  const theme = getThemeVars(result.overallScore);

  return (
    <div className="flex flex-col pb-8 animate-in slide-in-from-bottom-8 duration-300">
      
      {/* Header Banner */}
      <div className={`mb-6 p-4 border-4 border-black shadow-[6px_6px_0_0_#000] text-center bg-black`}>
        <h2 className={`text-3xl font-black ${theme.color} drop-shadow-[2px_2px_0_#fff]`}>
           {theme.icon} {theme.title} {theme.icon}
        </h2>
      </div>

      <div className="pixel-box bg-[#2f3542] overflow-hidden">
        
        {/* Score Header Section */}
        <div className="p-6 border-b-4 border-black bg-[#1e272e] flex flex-col sm:flex-row items-center gap-6">
          <div className="relative w-32 h-32 border-4 border-black shadow-[4px_4px_0_0_#000] shrink-0 bg-black">
            <img src={imageSrc} alt="Analyzed Target" className="w-full h-full object-cover filter contrast-125" />
            <div className={`absolute -bottom-4 -right-4 w-10 h-10 flex items-center justify-center border-4 border-black bg-white text-2xl shadow-[2px_2px_0_0_#000]`}>
              {theme.icon}
            </div>
          </div>

          <div className="flex-1 w-full">
            <h3 className="text-xl font-bold text-white mb-2 uppercase">HATE_LEVEL (怒氣值)</h3>
            <div className="flex items-baseline gap-2 mb-3">
              <span className={`text-6xl font-black ${theme.color} drop-shadow-[3px_3px_0_#000]`}>
                {result.overallScore}
              </span>
              <span className="text-xl text-[#a4b0be]">/ 100</span>
            </div>
            
            {/* Blocky Progress Bar */}
            <div className="w-full h-6 border-4 border-black bg-[#1a1520] p-0.5 flex">
              <div 
                className={`h-full ${theme.bg} transition-all duration-1000 ease-out`}
                style={{ width: `${result.overallScore}%` }}
              ></div>
            </div>
          </div>
        </div>

        {/* Content Section */}
        <div className="p-6 space-y-6">
          
          {/* Feature Pointers */}
          <div>
            <h3 className="text-xl font-bold mb-4 text-[#ff477e] drop-shadow-[1px_1px_0_#000]">
              ▶ SYSTEM_ANALYSIS
            </h3>
            <div className="space-y-4">
              {result.pointers.map((pointer, idx) => (
                <div key={idx} className="border-4 border-black bg-[#57606f] p-4 relative">
                  <div className="absolute -top-3 left-4 bg-black text-white px-2 py-0.5 border-2 border-black text-sm">
                    {pointer.feature}
                  </div>
                  <p className="text-white mt-2 leading-relaxed">{pointer.analysis}</p>
                </div>
              ))}
            </div>
          </div>

          {/* Overall Comment */}
          <div className="border-4 border-black bg-black p-4 relative">
            <h3 className="absolute -top-3 right-4 bg-black text-[#ffa502] px-2 py-0.5 border-2 border-[#ffa502] text-sm">
              STATUS
            </h3>
            <p className="text-[#dfe4ea] leading-relaxed mt-2 text-lg">
              {result.overallComment}
            </p>
          </div>

          {/* Recommendation */}
          <div className={`border-4 border-black bg-[#ff4757]/20 p-5 shadow-[inset_0_0_15px_rgba(255,71,87,0.3)]`}>
            <h3 className="text-xl font-bold mb-2 flex items-center gap-2 text-[#ff4757] drop-shadow-[1px_1px_0_#000]">
              ⚠️ SURVIVAL_GUIDE
            </h3>
            <p className="text-white leading-relaxed font-bold">
              {result.recommendation}
            </p>
          </div>

        </div>
      </div>

      <div className="mt-8">
        <button 
          onClick={onRetry}
          className="pixel-btn-neutral w-full text-white py-5 px-8 text-xl font-bold flex items-center justify-center gap-3"
        >
          🔄 RESET_SYSTEM (重新鑑定)
        </button>
      </div>
    </div>
  );
}