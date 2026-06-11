# Cenla-Door-website

import { useState } from "react";

/* ── Editable text primitive ── */
function E({ value, onChange, tag: Tag = "span", style = {}, multiline = false }) {
  const [editing, setEditing] = useState(false);
  const [draft, setDraft] = useState(value);
  const finish = () => { setEditing(false); if (draft.trim()) onChange(draft); else setDraft(value); };
  const shared = { fontFamily:"inherit",fontSize:"inherit",fontWeight:"inherit",lineHeight:"inherit",letterSpacing:"inherit",color:"inherit",background:"rgba(249,115,22,0.13)",border:"2px solid #F97316",borderRadius:4,outline:"none",padding:"2px 6px",width:"100%" };
  if (editing) return multiline
    ? <textarea autoFocus value={draft} onChange={e=>setDraft(e.target.value)} onBlur={finish} onKeyDown={e=>e.key==="Escape"&&finish()} style={{...shared,resize:"vertical",minHeight:64}} />
    : <input autoFocus value={draft} onChange={e=>setDraft(e.target.value)} onBlur={finish} onKeyDown={e=>(e.key==="Enter"||e.key==="Escape")&&finish()} style={shared} />;
  return (
    <Tag onClick={()=>setEditing(true)} title="Click to edit"
      style={{...style,cursor:"text",borderRadius:3,transition:"outline 0.1s"}}
      onMouseEnter={e=>e.currentTarget.style.outline="2px dashed rgba(249,115,22,0.55)"}
      onMouseLeave={e=>e.currentTarget.style.outline="none"}>
      {value.split("\n").map((l,i,a)=><span key={i}>{l}{i<a.length-1&&<br/>}</span>)}
    </Tag>
  );
}

/* ── Door SVG illustrations ── */
function CarriageDoor({color="#d4c4a8"}) {
  return (
    <svg viewBox="0 0 200 160" width="100%" height="160" style={{display:"block"}}>
      <rect width="200" height="160" fill={color} rx="2"/>
      {[0,40,80,120].map(y=>(
        <g key={y}>
          <rect x="4" y={y+4} width="90" height="34" fill="rgba(0,0,0,0.07)" rx="3"/>
          <rect x="106" y={y+4} width="90" height="34" fill="rgba(0,0,0,0.07)" rx="3"/>
          <path d={`M14 ${y+24} Q49 ${y+12} 84 ${y+24}`} fill="none" stroke="rgba(0,0,0,0.15)" strokeWidth="1.5"/>
          <path d={`M116 ${y+24} Q151 ${y+12} 186 ${y+24}`} fill="none" stroke="rgba(0,0,0,0.15)" strokeWidth="1.5"/>
        </g>
      ))}
      {[18,58,98,138].map(y=>(<g key={`h${y}`}><rect x="96" y={y} width="8" height="6" fill="#8B6914" rx="1"/></g>))}
      <circle cx="88" cy="82" r="5" fill="#8B6914"/>
      <circle cx="112" cy="82" r="5" fill="#8B6914"/>
      <line x1="100" y1="0" x2="100" y2="160" stroke="rgba(0,0,0,0.12)" strokeWidth="2"/>
      {[40,80,120].map(y=><line key={y} x1="0" x2="200" y1={y} y2={y} stroke="rgba(0,0,0,0.12)" strokeWidth="2"/>)}
    </svg>
  );
}
function TraditionalDoor({color="#c5d5e8"}) {
  return (
    <svg viewBox="0 0 200 160" width="100%" height="160" style={{display:"block"}}>
      <rect width="200" height="160" fill={color} rx="2"/>
      {[0,40,80,120].map(y=>(
        <g key={y}>
          <rect x="6" y={y+5} width="188" height="30" fill="rgba(0,0,0,0.06)" rx="2"/>
          {y===0 && [20,60,100,140].map(wx=>(<rect key={wx} x={wx} y={y+10} width="22" height="18" fill="rgba(255,255,255,0.55)" rx="1"/>))}
          <line x1="0" x2="200" y1={y+40} y2={y+40} stroke="rgba(0,0,0,0.1)" strokeWidth="2"/>
        </g>
      ))}
      <rect x="0" y="155" width="200" height="5" fill="rgba(0,0,0,0.15)"/>
    </svg>
  );
}
function ModernGlassDoor() {
  return (
    <svg viewBox="0 0 200 160" width="100%" height="160" style={{display:"block"}}>
      <rect width="200" height="160" fill="#2a2a2a" rx="2"/>
      {[0,38,76,114].map(y=>(
        <g key={y}>
          <rect x="0" y={y} width="200" height="6" fill="#555"/>
          <rect x="0" y={y+6} width="200" height="32" fill="rgba(135,200,235,0.35)"/>
          <rect x="10" y={y+8} width="40" height="28" fill="rgba(255,255,255,0.12)" rx="1"/>
        </g>
      ))}
      <rect x="0" y="152" width="200" height="8" fill="#555"/>
      <rect x="0" y="0" width="6" height="160" fill="#555"/>
      <rect x="194" y="0" width="6" height="160" fill="#555"/>
    </svg>
  );
}
function WoodCarriageDoor() {
  return (
    <svg viewBox="0 0 200 160" width="100%" height="160" style={{display:"block"}}>
      <rect width="200" height="160" fill="#8B5E3C" rx="2"/>
      {Array.from({length:20}).map((_,i)=>(<line key={i} x1="0" y1={i*8+4} x2="200" y2={i*8+2} stroke="rgba(0,0,0,0.08)" strokeWidth="1"/>))}
      {[0,40,80,120].map(y=>(
        <g key={y}>
          <rect x="8" y={y+6} width="82" height="28" fill="rgba(0,0,0,0.12)" rx="4"/>
          <rect x="110" y={y+6} width="82" height="28" fill="rgba(0,0,0,0.12)" rx="4"/>
          <line x1="0" x2="200" y1={y+40} y2={y+40} stroke="rgba(0,0,0,0.2)" strokeWidth="2"/>
        </g>
      ))}
      <line x1="100" y1="0" x2="100" y2="160" stroke="rgba(0,0,0,0.2)" strokeWidth="2"/>
      {[16,56,96,136].map(y=>(<rect key={y} x="90" y={y} width="20" height="8" fill="#2a2a2a" rx="1"/>))}
      <circle cx="86" cy="82" r="6" fill="none" stroke="#2a2a2a" strokeWidth="2.5"/>
      <circle cx="114" cy="82" r="6" fill="none" stroke="#2a2a2a" strokeWidth="2.5"/>
    </svg>
  );
}
function CommercialDoor() {
  return (
    <svg viewBox="0 0 200 160" width="100%" height="160" style={{display:"block"}}>
      <rect width="200" height="160" fill="#b0b8c1" rx="2"/>
      {Array.from({length:16}).map((_,i)=>(
        <g key={i}>
          <rect x="0" y={i*10} width="200" height="9" fill={i%2===0?"rgba(0,0,0,0.05)":"rgba(255,255,255,0.05)"}/>
          <line x1="0" x2="200" y1={i*10} y2={i*10} stroke="rgba(0,0,0,0.12)" strokeWidth="1"/>
        </g>
      ))}
      <rect x="0" y="0" width="10" height="160" fill="rgba(0,0,0,0.18)"/>
      <rect x="190" y="0" width="10" height="160" fill="rgba(0,0,0,0.18)"/>
      <rect x="0" y="150" width="200" height="10" fill="rgba(0,0,0,0.25)"/>
      <rect x="85" y="148" width="30" height="5" fill="#666" rx="2"/>
    </svg>
  );
}

/* ── Amarr door data ── */
const DOORS = [
  { id:"classica", name:"Amarr Classica", category:"Residential · Carriage House", tagline:"Authentic carriage-house style in stamped steel.", desc:"Over 100 authentic-looking carriage house designs permanently stamped in heavy-gauge steel. Available in triple-layer insulation with R-values up to 17.22. Whisper-quiet operation with Amarr's Quiet Door option.", features:["Triple-layer insulation","R-value up to 17.22","8 factory finish colors","Window insert options","WindPro wind-load rated"], illustration:<CarriageDoor/>, badge:"Most Popular" },
  { id:"heritage", name:"Amarr Heritage", category:"Residential · Traditional", tagline:"Classic, clean steel — built to last decades.", desc:"Four striking panel designs in heavy-gauge steel. Choose from traditional or raised-panel looks with countless window options and up to 6 base colors. Durable 5-layer paint system resists rust and fading.", features:["Single, double or triple-layer","R-value up to 12.76","6 base colors","Multiple panel designs","Optional window inserts"], illustration:<TraditionalDoor/>, badge:"Great Value" },
  { id:"horizon", name:"Amarr Horizon", category:"Residential · Modern Full View", tagline:"Floor-to-ceiling glass for a bold modern statement.", desc:"Aluminum frame with wide horizontal glass panes in transparent, frosted, or tinted glazing. Corrosion-resistant and engineered for durability. The go-to choice for contemporary homes and new builds.", features:["Aluminum & glass construction","Transparent, frost or tinted glass","Corrosion resistant","Tongue & groove joints","Multiple glazing options"], illustration:<ModernGlassDoor/>, badge:"Modern Style" },
  { id:"bydesign", name:"Amarr by Design", category:"Residential · Custom Wood", tagline:"Handcrafted wood doors built to your exact vision.", desc:"Handcrafted in 4 quality wood choices with optional distressing for a weathered look. Choose from 12 carriage house styles or design your own with custom trim overlays, arched windows, and decorative hardware.", features:["4 wood species","12 carriage house styles","Custom trim overlays","Arched or square windows","Decorative hardware"], illustration:<WoodCarriageDoor/>, badge:"Premium Custom" },
  { id:"commercial", name:"Amarr Commercial", category:"Commercial · Rolling Steel", tagline:"Heavy-duty doors that keep your business moving.", desc:"Full line of rolling sheet, rolling slat, and sectional steel doors for warehouses, loading docks, storage facilities, and retail storefronts. Engineered for high-cycle use with optional insulation and security features.", features:["Rolling sheet & slat options","High-cycle rated","Insulated & non-insulated","Fire-rated available","LiftMaster operator compatible"], illustration:<CommercialDoor/>, badge:"Commercial Grade" },
];

/* ── Mobile layout ── */
function MobileSite({c, set, setSvc, setWhy, activeDoor, setActiveDoor}) {
  const phone = c.phone.replace(/\D/g,"");
  return (
    <div style={{fontFamily:"'Inter','Segoe UI',sans-serif",background:"#F1F3F5",color:"#1C2B3A",maxWidth:430,margin:"0 auto"}}>
      {/* Mobile Nav */}
      <nav style={{background:"#1C2B3A",padding:"0 20px",height:56,display:"flex",alignItems:"center",justifyContent:"space-between",position:"sticky",top:0,zIndex:100}}>
        <E value={c.company} onChange={v=>set("company",v)} tag="span" style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:17,color:"#fff",letterSpacing:"0.5px"}}/>
        <a href={`tel:${phone}`} style={{background:"#F97316",color:"#fff",padding:"7px 14px",borderRadius:6,fontSize:13,fontWeight:700,textDecoration:"none",fontFamily:"'Oswald',sans-serif",letterSpacing:"0.5px"}}>Call Now</a>
      </nav>

      {/* Mobile Hero */}
      <section style={{background:"#1C2B3A",padding:"48px 24px 40px",textAlign:"center",position:"relative",overflow:"hidden"}}>
        <div style={{position:"absolute",inset:0,opacity:0.08,display:"grid",gridTemplateRows:"repeat(4,1fr)",gridTemplateColumns:"repeat(4,1fr)"}}>
          {Array.from({length:16}).map((_,i)=><div key={i} style={{border:"1px solid #F97316"}}/>)}
        </div>
        <div style={{display:"inline-block",background:"#F97316",color:"#fff",fontSize:10,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",padding:"4px 10px",borderRadius:3,marginBottom:16}}>Residential & Commercial</div>
        <E value={c.tagline} onChange={v=>set("tagline",v)} tag="h1" multiline style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:48,lineHeight:1.0,letterSpacing:"1px",color:"#fff",marginBottom:16,textTransform:"uppercase",display:"block"}}/>
        <E value={c.heroSub} onChange={v=>set("heroSub",v)} tag="p" style={{fontSize:14,color:"#94A3B8",lineHeight:1.7,marginBottom:28,display:"block"}}/>
        <a href={`tel:${phone}`} style={{display:"block",background:"#F97316",color:"#fff",padding:"16px",borderRadius:8,fontSize:18,fontWeight:700,fontFamily:"'Oswald',sans-serif",letterSpacing:"1px",textTransform:"uppercase",textDecoration:"none",marginBottom:12}}>
          Call for a Free Quote
        </a>
        <E value={c.phone} onChange={v=>set("phone",v)} tag="div" style={{color:"#F97316",fontSize:20,fontFamily:"'Oswald',sans-serif",fontWeight:700,letterSpacing:"1px"}}/>
      </section>

      {/* Mobile Services */}
      <section style={{padding:"40px 20px",background:"#fff"}}>
        <div style={{fontSize:11,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",color:"#F97316",marginBottom:8,textAlign:"center"}}>What We Do</div>
        <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:24,color:"#1C2B3A",textTransform:"uppercase",letterSpacing:"1px",textAlign:"center",marginBottom:24}}>Services</div>
        <div style={{display:"flex",flexDirection:"column",gap:14}}>
          {c.services.map((s,i)=>(
            <div key={i} style={{border:"1px solid #E2E8F0",borderRadius:10,padding:"18px 16px",borderLeft:"4px solid #F97316",display:"flex",gap:14,alignItems:"flex-start"}}>
              <span style={{fontSize:26,flexShrink:0}}>{s.icon}</span>
              <div>
                <E value={s.title} onChange={v=>setSvc(i,"title",v)} tag="div" style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:15,textTransform:"uppercase",letterSpacing:"0.5px",marginBottom:4,display:"block"}}/>
                <E value={s.desc} onChange={v=>setSvc(i,"desc",v)} tag="p" multiline style={{fontSize:13,color:"#64748B",lineHeight:1.6,margin:0}}/>
              </div>
            </div>
          ))}
        </div>
      </section>

      {/* Mobile Pricing */}
      <section style={{padding:"40px 20px",background:"#F1F3F5"}}>
        <div style={{fontSize:11,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",color:"#F97316",marginBottom:8,textAlign:"center"}}>Transparent Pricing</div>
        <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:24,color:"#1C2B3A",textTransform:"uppercase",letterSpacing:"1px",textAlign:"center",marginBottom:20}}>Service Call Rates</div>
        <div style={{background:"#1C2B3A",borderRadius:12,padding:"28px 24px",marginBottom:16,position:"relative",overflow:"hidden"}}>
          <div style={{position:"absolute",top:0,left:0,right:0,height:4,background:"#F97316"}}/>
          <div style={{fontSize:10,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",color:"#F97316",marginBottom:8}}>Inside Rapides Parish</div>
          <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:60,color:"#fff",lineHeight:1,marginBottom:4}}>$85</div>
          <div style={{fontSize:12,color:"#94A3B8",marginBottom:16}}>flat rate service call</div>
          {["Covers Alexandria, Pineville & all of Rapides Parish","Same-day dispatch when available","Service call applied toward any repair"].map(item=>(
            <div key={item} style={{display:"flex",gap:8,alignItems:"flex-start",marginBottom:8}}>
              <span style={{color:"#F97316",fontWeight:800,flexShrink:0}}>&#10003;</span>
              <span style={{fontSize:13,color:"#CBD5E1",lineHeight:1.5}}>{item}</span>
            </div>
          ))}
        </div>
        <div style={{background:"#fff",borderRadius:12,padding:"24px",border:"2px solid #E2E8F0"}}>
          <div style={{fontSize:10,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",color:"#64748B",marginBottom:8}}>Outside Rapides Parish</div>
          <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:28,color:"#1C2B3A",lineHeight:1,marginBottom:4}}>Call for Rate</div>
          <div style={{fontSize:12,color:"#94A3B8",marginBottom:14}}>priced based on mileage</div>
          {["We travel to surrounding parishes","Rate based on distance from Rapides Parish","Get a quote before we book your visit"].map(item=>(
            <div key={item} style={{display:"flex",gap:8,alignItems:"flex-start",marginBottom:8}}>
              <span style={{color:"#F97316",fontWeight:800,flexShrink:0}}>&#10003;</span>
              <span style={{fontSize:13,color:"#64748B",lineHeight:1.5}}>{item}</span>
            </div>
          ))}
          <a href={`tel:${phone}`} style={{display:"block",marginTop:16,background:"#F97316",color:"#fff",padding:"12px",borderRadius:6,fontSize:14,fontWeight:700,fontFamily:"'Oswald',sans-serif",letterSpacing:"0.5px",textTransform:"uppercase",textDecoration:"none",textAlign:"center"}}>
            Call for Travel Rate
          </a>
        </div>
      </section>

      {/* Mobile Door Picker */}
      <section style={{padding:"40px 20px",background:"#fff"}}>
        <div style={{fontSize:11,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",color:"#F97316",marginBottom:8,textAlign:"center"}}>Amarr Collection</div>
        <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:24,color:"#1C2B3A",textTransform:"uppercase",letterSpacing:"1px",textAlign:"center",marginBottom:20}}>Choose Your Door</div>
        <div style={{display:"flex",gap:10,overflowX:"auto",paddingBottom:4,marginBottom:20}}>
          {DOORS.map(d=>(
            <button key={d.id} onClick={()=>setActiveDoor(d)} style={{flex:"0 0 auto",width:110,background:"#fff",border:activeDoor.id===d.id?"3px solid #F97316":"2px solid #E2E8F0",borderRadius:8,padding:0,cursor:"pointer",overflow:"hidden",outline:"none"}}>
              <div>{d.illustration}</div>
              <div style={{padding:"6px 8px",background:activeDoor.id===d.id?"#FFF7ED":"#fff",borderTop:"1px solid #E2E8F0"}}>
                <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:10,textTransform:"uppercase",color:activeDoor.id===d.id?"#F97316":"#1C2B3A",lineHeight:1.3}}>{d.name.replace("Amarr ","")}</div>
              </div>
            </button>
          ))}
        </div>
        <div style={{background:"#1C2B3A",borderRadius:12,overflow:"hidden"}}>
          <div style={{padding:"20px"}}>{activeDoor.illustration}</div>
          <div style={{padding:"20px 24px",background:"#fff"}}>
            <div style={{fontSize:10,fontWeight:700,letterSpacing:"0.12em",textTransform:"uppercase",color:"#F97316",marginBottom:6}}>{activeDoor.category}</div>
            <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:22,color:"#1C2B3A",textTransform:"uppercase",marginBottom:4}}>{activeDoor.name}</div>
            <div style={{fontSize:13,fontWeight:600,color:"#64748B",marginBottom:12,fontStyle:"italic"}}>{activeDoor.tagline}</div>
            <p style={{fontSize:13,color:"#64748B",lineHeight:1.7,marginBottom:14}}>{activeDoor.desc}</p>
            <div style={{display:"flex",flexWrap:"wrap",gap:6,marginBottom:16}}>
              {activeDoor.features.map(f=>(
                <span key={f} style={{background:"#F1F3F5",border:"1px solid #E2E8F0",borderRadius:20,fontSize:11,fontWeight:500,color:"#1C2B3A",padding:"3px 10px"}}>&#10003; {f}</span>
              ))}
            </div>
            <a href={`tel:${phone}`} style={{display:"block",background:"#F97316",color:"#fff",padding:"13px",borderRadius:6,fontSize:14,fontWeight:700,fontFamily:"'Oswald',sans-serif",letterSpacing:"0.5px",textTransform:"uppercase",textDecoration:"none",textAlign:"center"}}>
              Get a Quote on This Door
            </a>
          </div>
        </div>
      </section>

      {/* Mobile Why Us */}
      <section style={{background:"#1C2B3A",padding:"40px 20px"}}>
        <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:24,color:"#fff",textTransform:"uppercase",letterSpacing:"1px",textAlign:"center",marginBottom:24}}>Why Choose Us?</div>
        <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:16}}>
          {c.whyItems.map((w,i)=>(
            <div key={i} style={{textAlign:"center",background:"rgba(255,255,255,0.05)",borderRadius:10,padding:"16px 12px"}}>
              <div style={{fontSize:24,marginBottom:8}}>{w.icon}</div>
              <E value={w.label} onChange={v=>setWhy(i,"label",v)} tag="div" style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:13,color:"#fff",textTransform:"uppercase",letterSpacing:"0.5px",marginBottom:6,display:"block"}}/>
              <E value={w.desc} onChange={v=>setWhy(i,"desc",v)} tag="p" multiline style={{fontSize:12,color:"#94A3B8",lineHeight:1.5}}/>
            </div>
          ))}
        </div>
      </section>

      {/* Mobile CTA */}
      <section style={{background:"#F97316",padding:"48px 24px",textAlign:"center"}}>
        <E value={c.ctaHeading} onChange={v=>set("ctaHeading",v)} tag="h2" style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:28,color:"#fff",textTransform:"uppercase",letterSpacing:"1px",marginBottom:12,lineHeight:1.1,display:"block"}}/>
        <E value={c.ctaSub} onChange={v=>set("ctaSub",v)} tag="p" style={{fontSize:14,color:"rgba(255,255,255,0.85)",lineHeight:1.7,marginBottom:24,display:"block"}}/>
        <a href={`tel:${phone}`} style={{display:"block",background:"#1C2B3A",color:"#fff",padding:"16px",borderRadius:8,fontSize:20,fontWeight:700,fontFamily:"'Oswald',sans-serif",letterSpacing:"1px",textTransform:"uppercase",textDecoration:"none",marginBottom:12}}>
          Call (318) 895-3160
        </a>
      </section>

      {/* Mobile Footer */}
      <footer style={{background:"#111B26",padding:"20px",textAlign:"center"}}>
        <E value={c.company} onChange={v=>set("company",v)} tag="div" style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:14,color:"#94A3B8",letterSpacing:"0.5px",marginBottom:6}}/>
        <E value={c.footerText} onChange={v=>set("footerText",v)} tag="div" style={{fontSize:11,color:"#475569"}}/>
      </footer>
    </div>
  );
}

/* ── Desktop layout ── */
function DesktopSite({c, set, setSvc, setWhy, activeDoor, setActiveDoor}) {
  return (
    <div style={{fontFamily:"'Inter','Segoe UI',sans-serif",background:"#F1F3F5",color:"#1C2B3A"}}>
      {/* Nav */}
      <nav style={{background:"#1C2B3A",padding:"0 40px",height:62,display:"flex",alignItems:"center",justifyContent:"space-between",position:"sticky",top:0,zIndex:100}}>
        <E value={c.company} onChange={v=>set("company",v)} tag="span" style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:20,color:"#fff",letterSpacing:"0.5px"}}/>
        <div style={{display:"flex",alignItems:"center",gap:20}}>
          {["Services","Doors","Pricing","Contact"].map(l=>(<a key={l} href={`#${l.toLowerCase()}`} style={{color:"#94A3B8",fontSize:14,fontWeight:500,textDecoration:"none"}} onMouseEnter={e=>e.target.style.color="#F97316"} onMouseLeave={e=>e.target.style.color="#94A3B8"}>{l}</a>))}
          <E value={c.phone} onChange={v=>set("phone",v)} tag="span" style={{background:"#F97316",color:"#fff",padding:"8px 18px",borderRadius:6,fontSize:14,fontWeight:700,fontFamily:"'Oswald',sans-serif",letterSpacing:"0.5px"}}/>
        </div>
      </nav>

      {/* Hero */}
      <section style={{background:"#1C2B3A",minHeight:"88vh",display:"flex",alignItems:"center",position:"relative",overflow:"hidden",padding:"80px 40px"}}>
        <div style={{position:"absolute",right:0,top:0,bottom:0,width:"44%",opacity:0.13,display:"grid",gridTemplateRows:"repeat(4,1fr)",gridTemplateColumns:"repeat(6,1fr)"}}>
          {Array.from({length:24}).map((_,i)=>(<div key={i} style={{border:"1px solid #F97316",borderRadius:2}}/>))}
        </div>
        <div style={{position:"absolute",top:40,right:40,background:"rgba(255,255,255,0.07)",border:"1px solid rgba(249,115,22,0.3)",borderRadius:8,padding:"10px 18px",textAlign:"center"}}>
          <div style={{fontSize:10,color:"#94A3B8",letterSpacing:"0.12em",textTransform:"uppercase",marginBottom:4}}>Authorized Dealer</div>
          <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:16,color:"#F97316",letterSpacing:"1px"}}>AMARR DOORS</div>
        </div>
        <div style={{maxWidth:660,position:"relative",zIndex:2}}>
          <div style={{display:"inline-block",background:"#F97316",color:"#fff",fontSize:11,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",padding:"5px 12px",borderRadius:3,marginBottom:24}}>Residential &amp; Commercial</div>
          <E value={c.tagline} onChange={v=>set("tagline",v)} tag="h1" multiline style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:"clamp(52px,8vw,92px)",lineHeight:1.0,letterSpacing:"1px",color:"#fff",marginBottom:28,textTransform:"uppercase",display:"block"}}/>
          <E value={c.heroSub} onChange={v=>set("heroSub",v)} tag="p" style={{fontSize:17,color:"#94A3B8",lineHeight:1.7,marginBottom:40,maxWidth:500,display:"block"}}/>
          <div style={{display:"flex",gap:16,flexWrap:"wrap",alignItems:"center"}}>
            <E value={c.heroCta} onChange={v=>set("heroCta",v)} tag="span" style={{background:"#F97316",color:"#fff",padding:"15px 34px",borderRadius:6,fontSize:15,fontWeight:700,fontFamily:"'Oswald',sans-serif",letterSpacing:"1px",textTransform:"uppercase",display:"inline-block"}}/>
            <E value={c.phone} onChange={v=>set("phone",v)} tag="span" style={{color:"#F97316",fontSize:24,fontFamily:"'Oswald',sans-serif",fontWeight:700,letterSpacing:"1px"}}/>
          </div>
        </div>
        <div style={{position:"absolute",left:0,bottom:0,right:0,height:5,background:"linear-gradient(90deg,#F97316 0%,#fb923c 50%,#1C2B3A 100%)"}}/>
      </section>

      {/* Services */}
      <section id="services" style={{background:"#fff",padding:"68px 40px"}}>
        <div style={{maxWidth:980,margin:"0 auto"}}>
          <div style={{textAlign:"center",marginBottom:48}}>
            <span style={{fontSize:11,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",color:"#F97316"}}>What We Do</span>
            <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:34,color:"#1C2B3A",marginTop:10,textTransform:"uppercase",letterSpacing:"1px"}}>Every Garage Door Need, Covered</div>
          </div>
          <div style={{display:"grid",gridTemplateColumns:"repeat(4,1fr)",gap:22}}>
            {c.services.map((s,i)=>(
              <div key={i} style={{border:"1px solid #E2E8F0",borderRadius:10,padding:"26px 20px",borderTop:"4px solid #F97316"}}>
                <div style={{fontSize:30,marginBottom:12}}>{s.icon}</div>
                <E value={s.title} onChange={v=>setSvc(i,"title",v)} tag="div" style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:17,textTransform:"uppercase",letterSpacing:"0.5px",marginBottom:8,display:"block"}}/>
                <E value={s.desc} onChange={v=>setSvc(i,"desc",v)} tag="p" multiline style={{fontSize:13,color:"#64748B",lineHeight:1.65}}/>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Pricing */}
      <section id="pricing" style={{background:"#F1F3F5",padding:"68px 40px"}}>
        <div style={{maxWidth:980,margin:"0 auto"}}>
          <div style={{textAlign:"center",marginBottom:48}}>
            <span style={{fontSize:11,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",color:"#F97316"}}>Transparent Pricing</span>
            <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:34,color:"#1C2B3A",marginTop:10,textTransform:"uppercase",letterSpacing:"1px"}}>Service Call Rates</div>
            <p style={{fontSize:14,color:"#64748B",marginTop:10}}>No hidden fees. You know the cost before we show up.</p>
          </div>
          <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:24,maxWidth:720,margin:"0 auto"}}>
            <div style={{background:"#1C2B3A",borderRadius:14,padding:"36px 32px",position:"relative",overflow:"hidden"}}>
              <div style={{position:"absolute",top:0,left:0,right:0,height:5,background:"#F97316"}}/>
              <div style={{fontSize:11,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",color:"#F97316",marginBottom:12}}>Residential &middot; Inside Rapides Parish</div>
              <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:64,color:"#fff",lineHeight:1,marginBottom:4}}>$85</div>
              <div style={{fontSize:13,color:"#94A3B8",marginBottom:24}}>flat rate service call</div>
              {["Covers Alexandria, Pineville & all of Rapides Parish","Technician dispatched same day when available","Service call fee applied toward any repair"].map(item=>(
                <div key={item} style={{display:"flex",gap:10,alignItems:"flex-start",marginBottom:10}}>
                  <span style={{color:"#F97316",fontWeight:800,flexShrink:0,marginTop:1}}>&#10003;</span>
                  <span style={{fontSize:13,color:"#CBD5E1",lineHeight:1.5}}>{item}</span>
                </div>
              ))}
            </div>
            <div style={{background:"#fff",borderRadius:14,padding:"36px 32px",position:"relative",overflow:"hidden",border:"2px solid #E2E8F0"}}>
              <div style={{position:"absolute",top:0,left:0,right:0,height:5,background:"#94A3B8"}}/>
              <div style={{fontSize:11,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",color:"#64748B",marginBottom:12}}>Residential &middot; Outside Rapides Parish</div>
              <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:40,color:"#1C2B3A",lineHeight:1,marginBottom:4}}>Call for Rate</div>
              <div style={{fontSize:13,color:"#94A3B8",marginBottom:24}}>priced based on mileage</div>
              {["We do travel to surrounding parishes","Rate determined by distance from Rapides Parish","Call us for a quick quote before booking"].map(item=>(
                <div key={item} style={{display:"flex",gap:10,alignItems:"flex-start",marginBottom:10}}>
                  <span style={{color:"#F97316",fontWeight:800,flexShrink:0,marginTop:1}}>&#10003;</span>
                  <span style={{fontSize:13,color:"#64748B",lineHeight:1.5}}>{item}</span>
                </div>
              ))}
              <div style={{marginTop:20,background:"#FFF7ED",border:"1px solid #FED7AA",borderRadius:8,padding:"12px 16px",fontSize:13,color:"#92400E"}}>
                <strong>Call (318) 895-3160</strong> and we'll give you a travel rate upfront — no surprises.
              </div>
            </div>
          </div>
          <p style={{textAlign:"center",fontSize:12,color:"#94A3B8",marginTop:20}}>* Service call covers diagnosis & travel. Repair labor and parts are quoted separately before any work begins.</p>
        </div>
      </section>

      {/* Door Selector */}
      <section id="doors" style={{background:"#fff",padding:"68px 40px"}}>
        <div style={{maxWidth:980,margin:"0 auto"}}>
          <div style={{textAlign:"center",marginBottom:40}}>
            <span style={{fontSize:11,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",color:"#F97316"}}>Amarr Door Collection</span>
            <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:34,color:"#1C2B3A",marginTop:10,textTransform:"uppercase",letterSpacing:"1px"}}>Choose Your Door Style</div>
            <p style={{fontSize:14,color:"#64748B",marginTop:10}}>We install the full Amarr lineup. Click any door below to learn more.</p>
          </div>
          <div style={{display:"flex",gap:12,marginBottom:32,overflowX:"auto",paddingBottom:4}}>
            {DOORS.map(d=>(
              <button key={d.id} onClick={()=>setActiveDoor(d)} style={{flex:"0 0 auto",width:150,background:"#fff",border:activeDoor.id===d.id?"3px solid #F97316":"2px solid #E2E8F0",borderRadius:10,padding:0,cursor:"pointer",overflow:"hidden",transition:"border 0.15s",outline:"none"}}>
                <div style={{overflow:"hidden"}}>{d.illustration}</div>
                <div style={{padding:"8px 10px",borderTop:"1px solid #E2E8F0",background:activeDoor.id===d.id?"#FFF7ED":"#fff"}}>
                  <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:12,textTransform:"uppercase",letterSpacing:"0.3px",color:activeDoor.id===d.id?"#F97316":"#1C2B3A",lineHeight:1.3}}>{d.name.replace("Amarr ","")}</div>
                  <div style={{fontSize:10,color:"#94A3B8",marginTop:2}}>{d.category.split(" · ")[0]}</div>
                </div>
              </button>
            ))}
          </div>
          <div style={{background:"#F1F3F5",borderRadius:14,overflow:"hidden",border:"1px solid #E2E8F0",display:"grid",gridTemplateColumns:"260px 1fr"}}>
            <div style={{background:"#1C2B3A",display:"flex",flexDirection:"column",alignItems:"center",justifyContent:"center",padding:24,gap:16}}>
              <div style={{width:"100%",borderRadius:8,overflow:"hidden",boxShadow:"0 4px 20px rgba(0,0,0,0.4)"}}>{activeDoor.illustration}</div>
              <span style={{background:"#F97316",color:"#fff",fontSize:11,fontWeight:700,letterSpacing:"0.1em",textTransform:"uppercase",padding:"4px 12px",borderRadius:20}}>{activeDoor.badge}</span>
            </div>
            <div style={{padding:"36px 40px",background:"#fff"}}>
              <div style={{fontSize:11,fontWeight:700,letterSpacing:"0.15em",textTransform:"uppercase",color:"#F97316",marginBottom:8}}>{activeDoor.category}</div>
              <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:30,color:"#1C2B3A",textTransform:"uppercase",letterSpacing:"0.5px",marginBottom:6}}>{activeDoor.name}</div>
              <div style={{fontSize:15,fontWeight:600,color:"#64748B",marginBottom:16,fontStyle:"italic"}}>{activeDoor.tagline}</div>
              <p style={{fontSize:14,color:"#64748B",lineHeight:1.75,marginBottom:24}}>{activeDoor.desc}</p>
              <div style={{display:"flex",flexWrap:"wrap",gap:8,marginBottom:28}}>
                {activeDoor.features.map(f=>(<span key={f} style={{background:"#F1F3F5",border:"1px solid #E2E8F0",borderRadius:20,fontSize:12,fontWeight:500,color:"#1C2B3A",padding:"4px 12px",display:"flex",alignItems:"center",gap:5}}><span style={{color:"#F97316",fontWeight:800}}>&#10003;</span>{f}</span>))}
              </div>
              <div style={{background:"#FFF7ED",border:"1px solid #FED7AA",borderRadius:8,padding:"14px 18px",fontSize:13,color:"#92400E"}}>
                &#128172; <strong>Interested in this door?</strong> Call us and we'll bring samples, measure your opening, and give you a free quote — no pressure.
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Why Us */}
      <section style={{background:"#1C2B3A",padding:"68px 40px"}}>
        <div style={{maxWidth:980,margin:"0 auto"}}>
          <div style={{textAlign:"center",marginBottom:48}}>
            <div style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:34,color:"#fff",textTransform:"uppercase",letterSpacing:"1px"}}>Why Choose Us?</div>
          </div>
          <div style={{display:"grid",gridTemplateColumns:"repeat(4,1fr)",gap:24}}>
            {c.whyItems.map((w,i)=>(
              <div key={i} style={{textAlign:"center",padding:"8px 12px"}}>
                <div style={{width:50,height:50,background:"#F97316",borderRadius:"50%",margin:"0 auto 14px",display:"flex",alignItems:"center",justifyContent:"center",fontSize:22}}>{w.icon}</div>
                <E value={w.label} onChange={v=>setWhy(i,"label",v)} tag="div" style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:15,color:"#fff",textTransform:"uppercase",letterSpacing:"0.5px",marginBottom:8,display:"block"}}/>
                <E value={w.desc} onChange={v=>setWhy(i,"desc",v)} tag="p" multiline style={{fontSize:13,color:"#94A3B8",lineHeight:1.6}}/>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* CTA */}
      <section id="contact" style={{background:"#F97316",padding:"76px 40px",textAlign:"center"}}>
        <div style={{maxWidth:660,margin:"0 auto"}}>
          <E value={c.ctaHeading} onChange={v=>set("ctaHeading",v)} tag="h2" style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:38,color:"#fff",textTransform:"uppercase",letterSpacing:"1px",marginBottom:14,lineHeight:1.1,display:"block"}}/>
          <E value={c.ctaSub} onChange={v=>set("ctaSub",v)} tag="p" style={{fontSize:16,color:"rgba(255,255,255,0.85)",lineHeight:1.7,marginBottom:34,display:"block"}}/>
          <div style={{display:"flex",gap:16,justifyContent:"center",flexWrap:"wrap",alignItems:"center"}}>
            <E value={c.heroCta} onChange={v=>set("heroCta",v)} tag="span" style={{background:"#1C2B3A",color:"#fff",padding:"15px 38px",borderRadius:6,fontSize:15,fontWeight:700,fontFamily:"'Oswald',sans-serif",letterSpacing:"1px",textTransform:"uppercase",display:"inline-block"}}/>
            <E value={c.phone} onChange={v=>set("phone",v)} tag="span" style={{color:"#fff",fontSize:26,fontFamily:"'Oswald',sans-serif",fontWeight:700,letterSpacing:"1px"}}/>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer style={{background:"#111B26",padding:"26px 40px",display:"flex",justifyContent:"space-between",alignItems:"center",flexWrap:"wrap",gap:12}}>
        <E value={c.company} onChange={v=>set("company",v)} tag="span" style={{fontFamily:"'Oswald',sans-serif",fontWeight:700,fontSize:16,color:"#94A3B8",letterSpacing:"0.5px"}}/>
        <E value={c.footerText} onChange={v=>set("footerText",v)} tag="span" style={{fontSize:12,color:"#475569"}}/>
        <E value={c.phone} onChange={v=>set("phone",v)} tag="span" style={{fontSize:14,color:"#F97316",fontFamily:"'Oswald',sans-serif",fontWeight:700,letterSpacing:"0.5px"}}/>
      </footer>
    </div>
  );
}

/* ── Root with view toggle ── */
export default function GarageSite() {
  const [view, setView] = useState("desktop");
  const [hint, setHint] = useState(true);
  const [activeDoor, setActiveDoor] = useState(DOORS[0]);

  const [c, setC] = useState({
    company:"Cenla Door Co.",
    phone:"(318) 895-3160",
    tagline:"Installed Right.\nFixed Fast.",
    heroSub:"Authorized Amarr dealer. Residential & commercial installation and repair. Same-day service available.",
    heroCta:"Call for a Free Quote",
    services:[
      {icon:"🔧",title:"Repairs",desc:"Broken springs, off-track doors, snapped cables — we fix it all, same day."},
      {icon:"🚪",title:"New Installations",desc:"We install any Amarr door style, size, and model for your home or business."},
      {icon:"⚡",title:"Opener Service",desc:"Garage door opener repair, replacement, and smart-home integration."},
      {icon:"🏗️",title:"Commercial Doors",desc:"Roll-up, sectional steel, high-speed doors for warehouses and businesses."},
    ],
    whyItems:[
      {label:"Same-Day Service",desc:"We answer the phone and show up when we say we will.",icon:"📞"},
      {label:"Licensed & Insured",desc:"Certified technicians, every job backed by warranty.",icon:"🏅"},
      {label:"Upfront Pricing",desc:"You get the price before we start — no surprises on the invoice.",icon:"💲"},
      {label:"Authorized Amarr Dealer",desc:"Factory-trained on every Amarr product with genuine parts.",icon:"✅"},
    ],
    ctaHeading:"Need a garage door fixed or installed?",
    ctaSub:"Call us today or request a quote and we'll get back to you within the hour.",
    footerText:"© 2026 Cenla Door Co. · Licensed & Insured · Authorized Amarr Dealer",
  });

  const set = (k,v)=>setC(p=>({...p,[k]:v}));
  const setSvc=(i,f,v)=>setC(p=>{const s=[...p.services];s[i]={...s[i],[f]:v};return{...p,services:s};});
  const setWhy=(i,f,v)=>setC(p=>{const w=[...p.whyItems];w[i]={...w[i],[f]:v};return{...p,whyItems:w};});

  const props = {c, set, setSvc, setWhy, activeDoor, setActiveDoor};

  return (
    <div>
      <style>{`@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@600;700&family=Inter:wght@400;500;600&display=swap');*{box-sizing:border-box;margin:0;padding:0;}`}</style>

      {/* Edit hint */}
      {hint && (
        <div style={{background:"#F97316",color:"#fff",textAlign:"center",padding:"9px 16px",fontSize:13,fontWeight:500,display:"flex",alignItems:"center",justifyContent:"center",gap:10,position:"sticky",top:0,zIndex:9999}}>
          &#9999;&#65039; Click any text to edit it — changes are instant
          <button onClick={()=>setHint(false)} style={{background:"rgba(255,255,255,0.25)",border:"none",color:"#fff",borderRadius:4,padding:"2px 10px",cursor:"pointer",fontSize:12}}>Got it</button>
        </div>
      )}

      {/* View Toggle Bar */}
      <div style={{background:"#0f1923",padding:"10px 0",display:"flex",justifyContent:"center",alignItems:"center",gap:8,position:"sticky",top:hint?37:0,zIndex:200,borderBottom:"1px solid #1e2d3d"}}>
        <span style={{fontSize:12,color:"#64748B",fontWeight:500,marginRight:4}}>View as:</span>
        <button
          onClick={()=>setView("desktop")}
          style={{display:"flex",alignItems:"center",gap:7,padding:"7px 18px",borderRadius:6,border:"none",cursor:"pointer",fontFamily:"'Inter',sans-serif",fontSize:13,fontWeight:600,transition:"all 0.15s",
            background:view==="desktop"?"#F97316":"rgba(255,255,255,0.06)",
            color:view==="desktop"?"#fff":"#94A3B8"}}>
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
            <rect x="2" y="3" width="20" height="14" rx="2"/><line x1="8" y1="21" x2="16" y2="21"/><line x1="12" y1="17" x2="12" y2="21"/>
          </svg>
          Desktop
        </button>
        <button
          onClick={()=>setView("mobile")}
          style={{display:"flex",alignItems:"center",gap:7,padding:"7px 18px",borderRadius:6,border:"none",cursor:"pointer",fontFamily:"'Inter',sans-serif",fontSize:13,fontWeight:600,transition:"all 0.15s",
            background:view==="mobile"?"#F97316":"rgba(255,255,255,0.06)",
            color:view==="mobile"?"#fff":"#94A3B8"}}>
          <svg width="14" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
            <rect x="5" y="2" width="14" height="20" rx="2"/><circle cx="12" cy="18" r="1"/>
          </svg>
          Mobile
        </button>
      </div>

      {/* Render chosen layout */}
      {view === "mobile" ? (
        <div style={{background:"#374151",minHeight:"100vh",padding:"24px 0",display:"flex",flexDirection:"column",alignItems:"center"}}>
          <div style={{fontSize:12,color:"#9CA3AF",marginBottom:16,fontWeight:500}}>Mobile Preview</div>
          <div style={{width:390,borderRadius:16,overflow:"hidden",boxShadow:"0 24px 60px rgba(0,0,0,0.5)",border:"6px solid #1C2B3A"}}>
            <MobileSite {...props}/>
          </div>
        </div>
      ) : (
        <DesktopSite {...props}/>
      )}
    </div>
  );
}
