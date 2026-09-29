import { useState, useEffect } from "react";
import {
  Coffee, Bike, MapPin, Heart, Sparkles, Navigation, Clock, Check, Instagram,
  Send, Music2, Leaf, Cookie, Flame, ChevronLeft, ChevronRight, Star, Snowflake, Cake,
} from "lucide-react";

const MENU = {
  "Класика": [
    { n: "Еспресso", d: "Спешелті, 18 г → 36 г", p: 55, i: Coffee },
    { n: "Флет уайт", d: "Double ristretto, молоко", p: 95, i: Coffee },
    { n: "Капучино", d: "Еспресо, щільна піна", p: 85, i: Coffee },
  ],
  "Авторська кава": [
    { n: "Фортечний", d: "Еспресо, карамель, морська сіль", p: 110, i: Flame },
    { n: "Смотрич", d: "Раф з лавандою та медом", p: 115, i: Sparkles },
    { n: "Мандрівний мед", d: "Флет уайт, гречаний мед, кориця", p: 105, i: Flame },
  ],
  "Холодні напої": [
    { n: "Cold brew", d: "16 год екстракції, лід", p: 95, i: Snowflake },
    { n: "Бамбл", d: "Еспресо, апельсиновий фреш, лід", p: 105, i: Snowflake },
    { n: "Айс-латте", d: "Еспресо, молоко, лід", p: 90, i: Snowflake },
  ],
  "Десерти": [
    { n: "Вівсяне печиво", d: "Печемо щоранку", p: 45, i: Cookie },
    { n: "Чізкейк Сан-Себастьян", d: "Порція, карамельний соус", p: 120, i: Cake },
    { n: "Гранола-бар", d: "Горіхи, мед, сухофрукти", p: 60, i: Cookie },
  ],
};

const SPOTS = [
  { id: 0, n: "Леопардовий міст, вул. Леонтовича", t: "08:00–11:00", h: [30, 90, 70, 20, 10], note: "Ранкова кава для тих, хто йде на роботу через міст." },
  { id: 1, n: "Парк Чекмана", t: "11:30–15:00", h: [10, 40, 85, 95, 50], note: "Лавки, тінь і холодні напої в спеку." },
  { id: 2, n: "Вхід до Старої фортеці", t: "15:30–20:00", h: [5, 20, 60, 100, 90], note: "Кава з видом на каньйон Смотрича." },
];
const HOURS = ["8:00", "11:00", "13:00", "16:00", "19:00"];

const QUIZ = [
  { q: "Який у тебе настрій?", o: ["Енергійний", "Спокійний", "Романтичний"] },
  { q: "Яка база напою?", o: ["Еспресо", "Молочна", "Холодна"] },
  { q: "Який смак ближчий?", o: ["Солодкий", "Фруктовий", "Гіркуватий"] },
];
const pick = (a) => {
  const m = a[1] === "Холодна" ? "Cold brew" : a[1] === "Молочна" ? (a[2] === "Солодкий" ? "Смотрич" : "Флет уайт") : a[2] === "Солодкий" ? "Фортечний" : a[2] === "Фруктовий" ? "Бамбл" : "Еспресо";
  const d = {
    "Cold brew": "Чистий, прохолодний і без гіркоти. Для довгої прогулянки бруківкою.",
    "Смотрич": "Ніжний раф з лавандою — для повільних кроків Старим містом.",
    "Флет уайт": "Насичений і збалансований. Тримає ритм, поки крутиш педалі.",
    "Фортечний": "Карамель із сіллю — солодкий заряд перед підйомом до фортеці.",
    "Бамбл": "Кава з апельсином: яскравий старт для енергійного дня.",
    "Еспресо": "Короткий і концентрований — швидка зупинка між локаціями.",
  };
  return { n: m, d: d[m] };
};

const REVIEWS = [
  { a: "Олена, Київ", t: "Випила флет уайт біля фортеці — найкраща кава за поїздку. Хлопці ще й підказали маршрут." },
  { a: "Тарас, Кам'янець", t: "Щоранку заїжджаю на Леонтовича. Кава швидка, смачна і без черг." },
  { a: "Anna, Warsaw", t: "Cold brew в парку — саме те. Дуже приємна атмосфера і велосипед на кухні." },
];

function useCount(target, run) {
  const [v, setV] = useState(0);
  useEffect(() => {
    if (!run) return;
    let f = 0;
    const id = setInterval(() => {
      f++;
      setV(Math.round(target * Math.min(f / 40, 1)));
      if (f >= 40) clearInterval(id);
    }, 30);
    return () => clearInterval(id);
  }, [target, run]);
  return v;
}

const Stat = ({ n, s, l }) => {
  const v = useCount(n, true);
  return (
    <div>
      <div className="text-4xl font-black text-orange-500">{v.toLocaleString("uk-UA")}{s}</div>
      <div className="text-sm text-stone-400 mt-1">{l}</div>
    </div>
  );
};

export default function CoffeeBike() {
  const [tab, setTab] = useState("Класика");
  const [favs, setFavs] = useState({});
  const [spot, setSpot] = useState(0);
  const [step, setStep] = useState(0);
  const [ans, setAns] = useState([]);
  const [rev, setRev] = useState(0);
  const [email, setEmail] = useState("");
  const [done, setDone] = useState(false);

  const totalFavs = Object.values(favs).filter(Boolean).length;
  const go = (id) => document.getElementById(id)?.scrollIntoView({ behavior: "smooth" });
  const answer = (o) => { setAns([...ans, o]); setStep(step + 1); };
  const reset = () => { setAns([]); setStep(0); };
  const res = step === 3 ? pick(ans) : null;
  const s = SPOTS[spot];

  const nav = [["menu", "Меню"], ["about", "Про нас"], ["quiz", "Квіз"], ["tracker", "Локації"], ["contacts", "Контакти"]];
  const wrap = "max-w-6xl mx-auto px-5";
  const btn = "rounded-full px-6 py-3 font-semibold transition active:scale-95";

  return (
    <div className="min-h-screen bg-stone-950 text-amber-50" style={{ background: "#1A1715", fontFamily: "Georgia, 'Times New Roman', serif" }}>
      {/* Header */}
      <header className="sticky top-0 z-30 backdrop-blur border-b border-white/10" style={{ background: "#1A1715ee" }}>
        <div className={`${wrap} flex items-center justify-between h-16 gap-3`}>
          <div className="flex items-center gap-2 font-black text-lg">
            <span className="relative"><Bike className="text-orange-500" size={26} /><Coffee className="absolute -top-1 -right-2 text-amber-200" size={12} /></span>
            Coffee Bike
          </div>
          <nav className="hidden md:flex gap-6 text-sm text-stone-300">
            {nav.map(([id, l]) => <button key={id} onClick={() => go(id)} className="hover:text-orange-400 transition">{l}</button>)}
          </nav>
          <button onClick={() => go("tracker")} className="text-xs sm:text-sm border border-orange-500/50 rounded-full px-3 py-1.5 flex items-center gap-2 hover:bg-orange-500/10">
            <span className="w-2 h-2 rounded-full bg-green-500 animate-pulse" /> Зараз на маршруті
          </button>
        </div>
      </header>

      {/* Hero */}
      <section className={`${wrap} py-16 md:py-24 grid md:grid-cols-2 gap-10 items-center`}>
        <div>
          <h1 className="text-5xl md:text-7xl font-black leading-[1.02]">Кава, яка рухає Кам'янець</h1>
          <p className="mt-6 text-lg text-stone-300 max-w-md">
            Спешелті-кава на колесах і затишна точка біля історичних пам'яток. Знайди нас — або чекай, поки ми приїдемо.
          </p>
          <div className="mt-8 flex flex-wrap gap-3">
            <button onClick={() => go("menu")} className={`${btn} bg-orange-500 text-stone-950 hover:bg-orange-400`}>Дивитися меню</button>
            <button onClick={() => go("tracker")} className={`${btn} border border-white/25 hover:border-orange-400`}>Де наш байк сьогодні?</button>
          </div>
        </div>
        <div className="rounded-3xl p-6 border border-white/10" style={{ background: "#241F1C" }}>
          <div className="flex items-center gap-2 text-orange-400 text-sm mb-4"><Navigation size={16} /> Байк зараз тут</div>
          <div className="text-2xl font-bold">{s.n}</div>
          <div className="flex items-center gap-2 text-stone-400 mt-1"><Clock size={15} /> {s.t}</div>
          <div className="mt-5 grid gap-2">
            {SPOTS.map((p) => (
              <button key={p.id} onClick={() => setSpot(p.id)}
                className={`text-left rounded-xl px-4 py-3 border transition ${spot === p.id ? "border-orange-500 bg-orange-500/10" : "border-white/10 hover:border-white/30"}`}>
                <MapPin size={14} className="inline mr-2 text-orange-400" />{p.n.split(",")[0]}
              </button>
            ))}
          </div>
        </div>
      </section>

      {/* About */}
      <section id="about" className="py-16" style={{ background: "#241F1C" }}>
        <div className={wrap}>
          <h2 className="text-3xl md:text-4xl font-black mb-10">Вайб Кам'янця</h2>
          <div className="grid sm:grid-cols-2 lg:grid-cols-4 gap-4">
            {[[Flame, "Свіже обсмажування", "Зерно від локальних обсмажувальників, не старше 2 тижнів."], [Bike, "Вело-доставка в парк", "Привеземо каву на лавку, де б ти не сидів."], [Leaf, "Екологічність", "Свій кубок — мінус 10 ₴. Компостовані стакани."], [Cookie, "Печиво & спешелті", "Домашня випічка до кожної чашки."]].map(([I, t, d]) => (
              <div key={t} className="rounded-2xl p-5 border border-white/10">
                <I className="text-orange-500 mb-3" />
                <div className="font-bold">{t}</div>
                <p className="text-sm text-stone-400 mt-1">{d}</p>
              </div>
            ))}
          </div>
          <div className="mt-12 grid grid-cols-2 gap-6 max-w-lg">
            <Stat n={10000} s="+" l="випитих чашок" />
            <Stat n={15} s=" км" l="веломаршрутів щодня" />
          </div>
        </div>
      </section>

      {/* Menu */}
      <section id="menu" className={`${wrap} py-16`}>
        <div className="flex items-end justify-between flex-wrap gap-3 mb-6">
          <h2 className="text-3xl md:text-4xl font-black">Меню</h2>
          <div className="flex items-center gap-2 text-sm text-stone-400"><Heart size={16} className="text-orange-500 fill-orange-500" /> В улюбленому: {totalFavs}</div>
        </div>
        <div className="flex gap-2 overflow-x-auto pb-2 mb-6">
          {Object.keys(MENU).map((k) => (
            <button key={k} onClick={() => setTab(k)}
              className={`whitespace-nowrap rounded-full px-5 py-2 text-sm font-semibold transition ${tab === k ? "bg-orange-500 text-stone-950" : "border border-white/15 hover:border-orange-400"}`}>{k}</button>
          ))}
        </div>
        <div className="grid sm:grid-cols-2 lg:grid-cols-3 gap-4">
          {MENU[tab].map((m) => {
            const on = favs[m.n];
            return (
              <div key={m.n} className="rounded-2xl p-5 border border-white/10 flex flex-col" style={{ background: "#241F1C" }}>
                <div className="w-12 h-12 rounded-xl bg-orange-500/15 grid place-items-center mb-4"><m.i className="text-orange-400" /></div>
                <div className="font-bold text-lg">{m.n}</div>
                <p className="text-sm text-stone-400 flex-1">{m.d}</p>
                <div className="flex items-center justify-between mt-4">
                  <span className="text-xl font-black text-orange-400">{m.p} ₴</span>
                  <button onClick={() => setFavs({ ...favs, [m.n]: !on })} aria-label="В улюблене" aria-pressed={!!on}
                    className="flex items-center gap-2 text-sm rounded-full border border-white/15 px-3 py-1.5 hover:border-orange-400">
                    <Heart size={16} className={`transition-transform duration-300 ${on ? "fill-orange-500 text-orange-500 scale-125" : "scale-100"}`} />
                    {on ? "В улюбленому" : "В улюблене"}
                  </button>
                </div>
              </div>
            );
          })}
        </div>
      </section>

      {/* Quiz */}
      <section id="quiz" className="py-16" style={{ background: "#241F1C" }}>
        <div className={`${wrap} max-w-2xl`}>
          <h2 className="text-3xl md:text-4xl font-black">Знайди свій напій для прогулянки Старим Містом</h2>
          <div className="mt-8 rounded-3xl border border-white/10 p-6" style={{ background: "#1A1715" }}>
            {step < 3 ? (
              <>
                <div className="flex gap-1 mb-5">{[0, 1, 2].map((i) => <div key={i} className={`h-1 flex-1 rounded ${i <= step ? "bg-orange-500" : "bg-white/10"}`} />)}</div>
                <div className="text-xl font-bold mb-4">{QUIZ[step].q}</div>
                <div className="grid gap-2">
                  {QUIZ[step].o.map((o) => <button key={o} onClick={() => answer(o)} className="text-left rounded-xl border border-white/15 px-4 py-3 hover:border-orange-400 hover:bg-orange-500/10 transition">{o}</button>)}
                </div>
              </>
            ) : (
              <div className="text-center">
                <Sparkles className="mx-auto text-orange-500 mb-3" />
                <div className="text-sm text-stone-400">Твій напій</div>
                <div className="text-3xl font-black my-2">{res.n}</div>
                <p className="text-stone-300 max-w-sm mx-auto">{res.d}</p>
                <div className="mt-6 flex justify-center gap-3 flex-wrap">
                  <button onClick={() => go("contacts")} className={`${btn} bg-orange-500 text-stone-950`}>Замовити</button>
                  <button onClick={reset} className={`${btn} border border-white/25`}>Пройти ще раз</button>
                </div>
              </div>
            )}
          </div>
        </div>
      </section>

      {/* Tracker */}
      <section id="tracker" className={`${wrap} py-16`}>
        <h2 className="text-3xl md:text-4xl font-black mb-8">Де наш байк сьогодні</h2>
        <div className="grid md:grid-cols-2 gap-6">
          <div className="relative rounded-3xl border border-white/10 h-72 overflow-hidden" style={{ background: "#241F1C" }}>
            <svg viewBox="0 0 300 200" className="absolute inset-0 w-full h-full" aria-hidden>
              <path d="M20 160 Q90 40 150 100 T280 40" fill="none" stroke="#F97316" strokeWidth="2" strokeDasharray="6 6" opacity=".5" />
            </svg>
            {[[16, 78], [48, 46], [86, 20]].map(([x, y], i) => (
              <button key={i} onClick={() => setSpot(i)} aria-label={SPOTS[i].n}
                className="absolute -translate-x-1/2 -translate-y-1/2" style={{ left: `${[7, 50, 93][i]}%`, top: `${[80, 50, 20][i]}%` }}>
                <span className={`grid place-items-center w-10 h-10 rounded-full transition ${spot === i ? "bg-orange-500 text-stone-950 scale-125" : "bg-stone-700 text-orange-300"}`}>
                  {spot === i ? <Bike size={18} /> : <MapPin size={18} />}
                </span>
              </button>
            ))}
          </div>
          <div className="rounded-3xl border border-white/10 p-6" style={{ background: "#241F1C" }}>
            <div className="font-bold text-lg">{s.n}</div>
            <div className="text-sm text-stone-400 mb-2">{s.t}</div>
            <p className="text-stone-300 text-sm mb-6">{s.note}</p>
            <div className="text-xs text-stone-400 mb-2">Скільки байк тут буває, %</div>
            <div className="flex items-end gap-3 h-32">
              {s.h.map((v, i) => (
                <div key={i} className="flex-1 flex flex-col items-center gap-1 h-full justify-end">
                  <div className="w-full rounded-t bg-orange-500 transition-all duration-500" style={{ height: `${v}%` }} />
                  <span className="text-[11px] text-stone-400">{HOURS[i]}</span>
                </div>
              ))}
            </div>
          </div>
        </div>
      </section>

      {/* Gallery & reviews */}
      <section className="py-16" style={{ background: "#241F1C" }}>
        <div className={wrap}>
          <h2 className="text-3xl md:text-4xl font-black mb-6">В Instagram</h2>
          <div className="grid grid-cols-2 md:grid-cols-4 gap-3">
            {[[Bike, "#7c2d12"], [Coffee, "#78350f"], [MapPin, "#431407"], [Sparkles, "#92400e"], [Coffee, "#451a03"], [Bike, "#9a3412"], [Cookie, "#78350f"], [Navigation, "#7c2d12"]].map(([I, c], i) => (
              <div key={i} className="aspect-square rounded-2xl grid place-items-center hover:scale-[1.03] transition" style={{ background: c }}>
                <I size={36} className="text-amber-200/70" />
              </div>
            ))}
          </div>
          <div className="mt-12 max-w-xl mx-auto text-center">
            <div className="flex justify-center gap-1 text-orange-400 mb-3">{[...Array(5)].map((_, i) => <Star key={i} size={16} className="fill-current" />)}</div>
            <p className="text-xl min-h-[6rem]">«{REVIEWS[rev].t}»</p>
            <div className="text-sm text-stone-400 mt-3">{REVIEWS[rev].a}</div>
            <div className="mt-4 flex justify-center gap-3">
              <button aria-label="Назад" onClick={() => setRev((rev + 2) % 3)} className="w-10 h-10 rounded-full border border-white/20 grid place-items-center hover:border-orange-400"><ChevronLeft size={18} /></button>
              <button aria-label="Далі" onClick={() => setRev((rev + 1) % 3)} className="w-10 h-10 rounded-full border border-white/20 grid place-items-center hover:border-orange-400"><ChevronRight size={18} /></button>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer id="contacts" className={`${wrap} py-16 grid md:grid-cols-2 gap-10`}>
        <div>
          <h2 className="text-3xl font-black">10-те горнятко — безкоштовно</h2>
          <p className="text-stone-400 mt-2">Залиш email — надішлемо картку лояльності.</p>
          {done ? (
            <div className="mt-5 flex items-center gap-3 rounded-2xl bg-green-500/15 border border-green-500/40 p-4">
              <span className="w-8 h-8 rounded-full bg-green-500 grid place-items-center text-stone-950"><Check size={18} /></span>
              Готово! Картка вже летить на {email}.
            </div>
          ) : (
            <div className="mt-5 flex gap-2 flex-col sm:flex-row">
              <input value={email} onChange={(e) => setEmail(e.target.value)} type="email" placeholder="you@email.com"
                className="flex-1 rounded-full px-5 py-3 bg-stone-900 border border-white/15 focus:outline-none focus:border-orange-500" />
              <button disabled={!/\S+@\S+\.\S+/.test(email)} onClick={() => setDone(true)}
                className={`${btn} bg-orange-500 text-stone-950 disabled:opacity-40`}>Отримати картку</button>
            </div>
          )}
        </div>
        <div className="text-stone-300 space-y-2">
          <div className="font-bold text-amber-50">Кавовий хаб</div>
          <div className="flex gap-2"><MapPin size={16} className="text-orange-500 mt-1 shrink-0" /> Кам'янець-Подільський, вул. Троїцька, 1 (уточніть адресу)</div>
          <div className="flex gap-2"><Clock size={16} className="text-orange-500 mt-1 shrink-0" /> Щодня 08:00–20:00</div>
          <div className="flex gap-3 pt-3">
            {[[Instagram, "Instagram"], [Send, "Telegram"], [Music2, "TikTok"]].map(([I, l]) => (
              <a key={l} href="#" aria-label={l} className="w-10 h-10 rounded-full border border-white/20 grid place-items-center hover:border-orange-400 hover:text-orange-400"><I size={18} /></a>
            ))}
          </div>
        </div>
      </footer>
    </div>
  );
}
