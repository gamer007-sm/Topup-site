import React, { useState } from 'react';
import { 
  Gamepad2, Wallet, History, Settings,
  CheckCircle2, ArrowRight, Gift, ShieldAlert
} from 'lucide-react';

export default function App() {
  const [activeTab, setActiveTab] = useState('home');
  const [walletBalance, setWalletBalance] = useState(500);
  const [rewardPoints, setRewardPoints] = useState(120);

  // Top-Up Form State
  const [selectedGame, setSelectedGame] = useState('ff');
  const [playerId, setPlayerId] = useState('');
  const [selectedPack, setSelectedPack] = useState(null);
  const [paymentMethod, setPaymentMethod] = useState('direct');
  const [trxId, setTrxId] = useState('');

  // Sample Data
  const diamondPacks = [
    { id: 1, amount: '115 Diamonds', price: 80, tag: 'Popular' },
    { id: 2, amount: '240 Diamonds', price: 160, tag: '' },
    { id: 3, amount: '610 Diamonds', price: 400, tag: 'Best Value' },
    { id: 4, amount: '1240 Diamonds', price: 800, tag: 'Bonus +50' }
  ];

  return (
    <div className="min-h-screen bg-[#0b0e14] text-slate-100 font-sans pb-12">
      
      {/* 🧭 1. Header / Navbar */}
      <nav className="sticky top-0 z-50 bg-[#0f172a]/80 backdrop-blur-md border-b border-slate-800 px-4 py-3">
        <div className="max-w-6xl mx-auto flex justify-between items-center">
          <div className="flex items-center gap-2 cursor-pointer" onClick={() => setActiveTab('home')}>
            <div className="bg-gradient-to-tr from-violet-600 to-cyan-400 p-2 rounded-xl text-white shadow-[0_0_15px_rgba(139,92,246,0.5)]">
              <Gamepad2 className="w-6 h-6" />
            </div>
            <span className="text-xl font-extrabold tracking-wider bg-clip-text text-transparent bg-gradient-to-r from-violet-400 to-cyan-400">
              GAMEZONE
            </span>
          </div>

          <div className="flex items-center gap-3">
            <button 
              onClick={() => setActiveTab('wallet')} 
              className="flex items-center gap-2 bg-slate-800/80 hover:bg-slate-700/80 border border-slate-700 px-3 py-1.5 rounded-lg text-sm transition">
              <Wallet className="w-4 h-4 text-cyan-400" />
              <span className="font-semibold text-cyan-300">৳{walletBalance}</span>
            </button>

            <button 
              onClick={() => setActiveTab('admin')} 
              className="p-2 bg-slate-800/80 hover:bg-slate-700/80 border border-slate-700 rounded-lg text-slate-400 hover:text-white transition">
              <Settings className="w-5 h-5" />
            </button>
          </div>
        </div>
      </nav>

      <div className="max-w-6xl mx-auto px-4 mt-6">
        
        {/* 📌 2. Navigation Tabs */}
        <div className="flex gap-2 border-b border-slate-800 pb-3 mb-6 overflow-x-auto">
          <button 
            onClick={() => setActiveTab('home')}
            className={`flex items-center gap-2 px-4 py-2 rounded-lg text-sm font-medium transition ${activeTab === 'home' ? 'bg-violet-600 text-white shadow-lg shadow-violet-600/30' : 'bg-slate-900/60 text-slate-400 hover:text-white'}`}>
            <Gamepad2 className="w-4 h-4" /> Top-Up Store
          </button>
          <button 
            onClick={() => setActiveTab('wallet')}
            className={`flex items-center gap-2 px-4 py-2 rounded-lg text-sm font-medium transition ${activeTab === 'wallet' ? 'bg-violet-600 text-white shadow-lg shadow-violet-600/30' : 'bg-slate-900/60 text-slate-400 hover:text-white'}`}>
            <Wallet className="w-4 h-4" /> My Wallet & Rewards
          </button>
          <button 
            onClick={() => setActiveTab('orders')}
            className={`flex items-center gap-2 px-4 py-2 rounded-lg text-sm font-medium transition ${activeTab === 'orders' ? 'bg-violet-600 text-white shadow-lg shadow-violet-600/30' : 'bg-slate-900/60 text-slate-400 hover:text-white'}`}>
            <History className="w-4 h-4" /> Order History
          </button>
          <button 
            onClick={() => setActiveTab('admin')}
            className={`flex items-center gap-2 px-4 py-2 rounded-lg text-sm font-medium transition ${activeTab === 'admin' ? 'bg-cyan-600 text-white shadow-lg shadow-cyan-600/30' : 'bg-slate-900/60 text-slate-400 hover:text-white'}`}>
            <Settings className="w-4 h-4" /> Admin Controls
          </button>
        </div>

        {/* ------------------- PAGE 1: HOME / TOP-UP STORE ------------------- */}
        {activeTab === 'home' && (
          <div className="space-y-6">
            {/* Banner Slider Placeholder */}
            <div className="bg-gradient-to-r from-violet-900/40 via-purple-900/20 to-cyan-900/40 border border-violet-500/30 rounded-2xl p-6 relative overflow-hidden flex items-center justify-between">
              <div>
                <span className="bg-violet-500/20 text-violet-300 text-xs px-3 py-1 rounded-full font-semibold border border-violet-500/30">🔥 SPECIAL OFFER</span>
                <h2 className="text-2xl font-bold mt-2">Get Extra 10% Diamond Cashback!</h2>
                <p className="text-slate-400 text-sm mt-1">Pay using Wallet Deposit & get instant discount points.</p>
              </div>
              <Gift className="w-20 h-20 text-violet-400/30 absolute right-4 bottom-2" />
            </div>

            {/* Step 1: Select Game */}
            <div className="bg-slate-900/60 backdrop-blur-md border border-slate-800 rounded-2xl p-5">
              <h3 className="text-lg font-semibold mb-4 text-cyan-400 flex items-center gap-2">
                <span className="bg-cyan-400/10 p-1.5 rounded-lg text-cyan-400">1</span> Select Game Category
              </h3>
              <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
                <div 
                  onClick={() => setSelectedGame('ff')}
                  className={`cursor-pointer rounded-xl p-4 border transition flex flex-col items-center gap-2 ${selectedGame === 'ff' ? 'border-violet-500 bg-violet-500/10 shadow-[0_0_15px_rgba(139,92,246,0.2)]' : 'border-slate-800 bg-slate-900/40 hover:border-slate-700'}`}>
                  <div className="text-3xl">💎</div>
                  <div className="font-bold text-center">Free Fire</div>
                  <span className="text-xs text-emerald-400 bg-emerald-400/10 px-2 py-0.5 rounded">Auto Delivery</span>
                </div>
                <div 
                  onClick={() => setSelectedGame('pubg')}
                  className={`cursor-pointer rounded-xl p-4 border transition flex flex-col items-center gap-2 ${selectedGame === 'pubg' ? 'border-violet-500 bg-violet-500/10 shadow-[0_0_15px_rgba(139,92,246,0.2)]' : 'border-slate-800 bg-slate-900/40 hover:border-slate-700'}`}>
                  <div className="text-3xl">🔫</div>
                  <div className="font-bold text-center">PUBG Mobile UC</div>
                  <span className="text-xs text-cyan-400 bg-cyan-400/10 px-2 py-0.5 rounded">Instant API</span>
                </div>
              </div>
            </div>

            {/* Step 2: Player ID & Verification */}
            <div className="bg-slate-900/60 backdrop-blur-md border border-slate-800 rounded-2xl p-5">
              <h3 className="text-lg font-semibold mb-3 text-cyan-400 flex items-center gap-2">
                <span className="bg-cyan-400/10 p-1.5 rounded-lg text-cyan-400">2</span> Enter Player ID (UID)
              </h3>
              <div className="relative">
                <input 
                  type="text" 
                  value={playerId}
                  onChange={(e) => setPlayerId(e.target.value)}
                  placeholder="e.g. 123456789" 
                  className="w-full bg-slate-950 border border-slate-800 rounded-xl px-4 py-3 text-slate-100 focus:outline-none focus:border-violet-500 transition"
                />
              </div>
              <p className="text-xs text-slate-500 mt-2 flex items-center gap-1">
                <ShieldAlert className="w-3.5 h-3.5 text-amber-500" /> 
                ৩ বারের বেশি ভুল আইডি দিলে অর্ডার বাতিল হবে। ১০ বার ভুলের ক্ষেত্রে অ্যাকাউন্ট থেকে পেনাল্টি কাটবে।
              </p>
            </div>

            {/* Step 3: Select Package */}
            <div className="bg-slate-900/60 backdrop-blur-md border border-slate-800 rounded-2xl p-5">
              <h3 className="text-lg font-semibold mb-4 text-cyan-400 flex items-center gap-2">
                <span className="bg-cyan-400/10 p-1.5 rounded-lg text-cyan-400">3</span> Select Recharge Package
              </h3>
              <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
                {diamondPacks.map((pack) => (
                  <div 
                    key={pack.id}
                    onClick={() => setSelectedPack(pack)}
                    className={`cursor-pointer rounded-xl p-4 border relative transition flex flex-col justify-between ${selectedPack?.id === pack.id ? 'border-violet-500 bg-violet-500/10 shadow-[0_0_15px_rgba(139,92,246,0.3)]' : 'border-slate-800 bg-slate-950/50 hover:border-slate-700'}`}>
                    {pack.tag && (
                      <span className="absolute -top-2.5 right-3 bg-gradient-to-r from-violet-600 to-cyan-500 text-[10px] font-bold px-2 py-0.5 rounded-full uppercase tracking-wider text-white">
                        {pack.tag}
                      </span>
                    )}
                    <div className="font-semibold text-slate-200">{pack.amount}</div>
                    <div className="text-xl font-extrabold text-cyan-400 mt-2">৳{pack.price}</div>
                  </div>
                ))}
              </div>
            </div>

            {/* Step 4: Payment Method */}
            <div className="bg-slate-900/60 backdrop-blur-md border border-slate-800 rounded-2xl p-5">
              <h3 className="text-lg font-semibold mb-4 text-cyan-400 flex items-center gap-2">
                <span className="bg-cyan-400/10 p-1.5 rounded-lg text-cyan-400">4</span> Choose Payment Option
              </h3>
              
              <div className="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                <label className={`cursor-pointer border rounded-xl p-4 flex items-center justify-between transition ${paymentMethod === 'direct' ? 'border-violet-500 bg-violet-500/10' : 'border-slate-800 bg-slate-950/40'}`}>
                  <div className="flex items-center gap-3">
                    <input type="radio" name="pay" checked={paymentMethod === 'direct'} onChange={() => setPaymentMethod('direct')} className="accent-violet-500" />
                    <div>
                      <div className="font-semibold">Direct Personal bKash</div>
                      <div className="text-xs text-slate-400">Send Money + Auto SMS Verification</div>
                    </div>
                  </div>
                  <span className="text-pink-500 font-bold text-sm">bKash</span>
                </label>

                <label className={`cursor-pointer border rounded-xl p-4 flex items-center justify-between transition ${paymentMethod === 'wallet' ? 'border-violet-500 bg-violet-500/10' : 'border-slate-800 bg-slate-950/40'}`}>
                  <div className="flex items-center gap-3">
                    <input type="radio" name="pay" checked={paymentMethod === 'wallet'} onChange={() => setPaymentMethod('wallet')} className="accent-violet-500" />
                    <div>
                      <div className="font-semibold">Account Wallet</div>
                      <div className="text-xs text-slate-400">Available: ৳{walletBalance}</div>
                    </div>
                  </div>
                  <Wallet className="w-5 h-5 text-cyan-400" />
                </label>
              </div>

              {/* Direct bKash TrxID Input Box */}
              {paymentMethod === 'direct' && (
                <div className="p-4 bg-slate-950 border border-slate-800 rounded-xl space-y-3">
                  <p className="text-xs text-slate-300">
                    Send Money to: <span className="font-mono text-cyan-400 bg-slate-900 px-2 py-0.5 rounded">017XXXXXXXX</span> (Personal)
                  </p>
                  <input 
                    type="text" 
                    value={trxId}
                    onChange={(e) => setTrxId(e.target.value)}
                    placeholder="Enter bKash Transaction ID (TrxID)" 
                    className="w-full bg-slate-900 border border-slate-800 rounded-lg px-3 py-2 text-sm text-slate-100 focus:outline-none focus:border-violet-500"
                  />
                </div>
              )}

              {/* Submit Button */}
              <button className="w-full mt-6 bg-gradient-to-r from-violet-600 to-cyan-500 hover:from-violet-500 hover:to-cyan-400 text-white font-bold py-3.5 rounded-xl shadow-[0_0_20px_rgba(139,92,246,0.4)] transition flex items-center justify-center gap-2">
                Pay & Instant Order Now <ArrowRight className="w-5 h-5" />
              </button>
            </div>
          </div>
        )}

        {/* ------------------- PAGE 2: WALLET & REWARDS ------------------- */}
        {activeTab === 'wallet' && (
          <div className="space-y-6">
            <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
              {/* Wallet Balance Card */}
              <div className="bg-slate-900/60 border border-slate-800 rounded-2xl p-6">
                <span className="text-xs text-slate-400">Current Wallet Balance</span>
                <div className="text-4xl font-extrabold text-cyan-400 mt-1">৳{walletBalance}.00</div>
                
                <div className="mt-6 pt-6 border-t border-slate-800">
                  <h4 className="font-semibold text-sm mb-3">Deposit Balance (bKash)</h4>
                  <div className="space-y-3">
                    <input type="number" placeholder="Enter Amount (৳)" className="w-full bg-slate-950 border border-slate-800 rounded-lg px-3 py-2 text-sm" />
                    <input type="text" placeholder="Transaction ID (TrxID)" className="w-full bg-slate-950 border border-slate-800 rounded-lg px-3 py-2 text-sm" />
                    <button className="w-full bg-violet-600 hover:bg-violet-500 text-white font-semibold py-2 rounded-lg text-sm transition">
                      Add Money to Wallet
                    </button>
                  </div>
                </div>
              </div>

              {/* Loyalty Rewards Card */}
              <div className="bg-slate-900/60 border border-slate-800 rounded-2xl p-6 flex flex-col justify-between">
                <div>
                  <div className="flex justify-between items-start">
                    <div>
                      <span className="text-xs text-slate-400">Your Reward Points</span>
                      <div className="text-3xl font-bold text-amber-400 mt-1">{rewardPoints} PTS</div>
                    </div>
                    <Gift className="w-8 h-8 text-amber-400" />
                  </div>
                  <p className="text-xs text-slate-400 mt-4">
                    Get reward points on every top-up & daily login. Convert points directly into wallet balance!
                  </p>
                </div>

                <div className="mt-6 pt-4 border-t border-slate-800">
                  <button className="w-full bg-amber-500/10 border border-amber-500/30 text-amber-400 font-semibold py-2 rounded-lg text-sm hover:bg-amber-500/20 transition">
                    Convert 100 PTS to ৳5 Balance
                  </button>
                </div>
              </div>
            </div>
          </div>
        )}

        {/* ------------------- PAGE 3: ORDER HISTORY ------------------- */}
        {activeTab === 'orders' && (
          <div className="bg-slate-900/60 border border-slate-800 rounded-2xl p-5">
            <h3 className="text-lg font-semibold mb-4">Recent Top-Up Orders</h3>
            <div className="space-y-3">
              <div className="bg-slate-950 border border-slate-800 rounded-xl p-4 flex justify-between items-center">
                <div>
                  <div className="font-bold">115 Free Fire Diamonds</div>
                  <div className="text-xs text-slate-400 mt-0.5">UID: 987654321 | TrxID: BK892374</div>
                </div>
                <div className="text-right">
                  <span className="bg-emerald-500/10 text-emerald-400 border border-emerald-500/20 text-xs px-2.5 py-1 rounded-full font-semibold flex items-center gap-1">
                    <CheckCircle2 className="w-3 h-3" /> Completed
                  </span>
                  <div className="text-xs text-slate-500 mt-1">৳80.00</div>
                </div>
              </div>

              <div className="bg-slate-950 border border-slate-800 rounded-xl p-4 flex justify-between items-center">
                <div>
                  <div className="font-bold">60 PUBG UC</div>
                  <div className="text-xs text-slate-400 mt-0.5">UID: 554433221 | TrxID: BK901122</div>
                </div>
                <div className="text-right">
                  <span className="bg-amber-500/10 text-amber-400 border border-amber-500/20 text-xs px-2.5 py-1 rounded-full font-semibold">
                    Processing (Semi-Auto)
                  </span>
                  <div className="text-xs text-slate-500 mt-1">৳95.00</div>
                </div>
              </div>
            </div>
          </div>
        )}

        {/* ------------------- PAGE 4: ADMIN CONTROLS ------------------- */}
        {activeTab === 'admin' && (
          <div className="bg-slate-900/60 border border-slate-800 rounded-2xl p-6 space-y-6">
            <div className="flex justify-between items-center border-b border-slate-800 pb-4">
              <h3 className="text-lg font-bold text-cyan-400">Admin Controls & Customization</h3>
              <span className="bg-violet-500/20 text-violet-300 text-xs px-3 py-1 rounded-full font-mono">Owner Panel</span>
            </div>

            <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
              {/* Reward Customizer */}
              <div className="bg-slate-950 border border-slate-800 rounded-xl p-4 space-y-3">
                <h4 className="font-semibold text-sm text-slate-200">🎁 Reward Points Customization</h4>
                <div>
                  <label className="text-xs text-slate-400">Daily Login Bonus (PTS)</label>
                  <input type="number" defaultValue={10} className="w-full bg-slate-900 border border-slate-800 rounded px-3 py-1.5 text-sm mt-1" />
                </div>
                <div>
                  <label className="text-xs text-slate-400">Points per ৳100 Purchase</label>
                  <input type="number" defaultValue={5} className="w-full bg-slate-900 border border-slate-800 rounded px-3 py-1.5 text-sm mt-1" />
                </div>
                <button className="bg-violet-600 text-xs px-3 py-2 rounded font-semibold text-white">Save Reward Settings</button>
              </div>

              {/* Automation Engine Toggle */}
              <div className="bg-slate-950 border border-slate-800 rounded-xl p-4 space-y-3">
                <h4 className="font-semibold text-sm text-slate-200">🤖 Hybrid Supplier Engine</h4>
                <div className="flex items-center justify-between">
                  <span className="text-xs text-slate-300">Auto-API Order Execution</span>
                  <input type="checkbox" className="toggle accent-cyan-400" defaultChecked />
                </div>
                <p className="text-[11px] text-slate-500">
                  সাপ্লায়ার ব্যাকএন্ডে ডিপোজিট ব্যালেন্স না থাকলে এটি স্বয়ংক্রিয়ভাবে জিরো-ইনভেস্টমেন্ট সেমি-অটো মোডে স্যুইচ করবে।
                </p>
              </div>
            </div>
          </div>
        )}

      </div>
    </div>
  );
}