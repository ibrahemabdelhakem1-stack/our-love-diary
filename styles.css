import { useState, useEffect } from "react";
import { motion, AnimatePresence } from "framer-motion";
import { initializeApp } from "firebase/app";
import { getFirestore, collection, addDoc, onSnapshot, deleteDoc, doc } from "firebase/firestore";

const firebaseConfig = {
  apiKey: "AIzaSyC3Ladq9dC6YkBZ83fZMj-yXm0QCLHjj5M",
  authDomain: "love-dairy-85ca3.firebaseapp.com",
  projectId: "love-dairy-85ca3",
  storageBucket: "love-dairy-85ca3.firebasestorage.app",
  messagingSenderId: "218352996251",
  appId: "1:218352996251:web:fa3d932a149b66e3cbdb3e"
};

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

// 🎬 CINEMATIC CAROUSEL
function ImageCarousel({ images }) {
  const [index, setIndex] = useState(0);

  const next = () => setIndex((prev) => (prev + 1) % images.length);
  const prev = () => setIndex((prev) => (prev - 1 + images.length) % images.length);

  return (
    <div style={{ position: "relative", height: "260px", marginBottom: "15px", borderRadius: "20px", overflow: "hidden", boxShadow: "0 10px 30px rgba(0,0,0,0.2)" }}>
      <AnimatePresence>
        <motion.img
          key={index}
          src={images[index]}
          style={{ width: "100%", height: "100%", objectFit: "cover", position: "absolute" }}
          initial={{ opacity: 0, scale: 1.05 }}
          animate={{ opacity: 1, scale: 1 }}
          exit={{ opacity: 0 }}
          transition={{ duration: 0.5 }}
        />
      </AnimatePresence>

      {images.length > 1 && (
        <>
          <button onClick={prev} style={{ position: "absolute", left: 10, top: "50%", background: "rgba(0,0,0,0.5)", color: "white", borderRadius: "50%", padding: "5px 10px" }}>◀</button>
          <button onClick={next} style={{ position: "absolute", right: 10, top: "50%", background: "rgba(0,0,0,0.5)", color: "white", borderRadius: "50%", padding: "5px 10px" }}>▶</button>
        </>
      )}
    </div>
  );
}

export default function LoveDiary() {
  const [authorized, setAuthorized] = useState(false);
  const [password, setPassword] = useState("");
  const [error, setError] = useState("");

  const [memories, setMemories] = useState([]);
  const [text, setText] = useState("");
  const [images, setImages] = useState([]);

  const [time, setTime] = useState({ days: 0, hours: 0, minutes: 0, seconds: 0 });

  const startDate = new Date("2025-11-28T00:00:00");

  const correctPassword = "28112025";

  useEffect(() => {
    const unsub = onSnapshot(collection(db, "memories"), (snapshot) => {
      setMemories(snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() })));
    });
    return () => unsub();
  }, []);

  useEffect(() => {
    if (!authorized) return;

    const interval = setInterval(() => {
      const now = new Date();
      const diff = now - startDate;

      setTime({
        days: Math.floor(diff / (1000 * 60 * 60 * 24)),
        hours: Math.floor(diff / (1000 * 60 * 60)) % 24,
        minutes: Math.floor(diff / (1000 * 60)) % 60,
        seconds: Math.floor(diff / 1000) % 60
      });
    }, 1000);

    return () => clearInterval(interval);
  }, [authorized]);

  const handleLogin = () => {
    if (password === correctPassword) setAuthorized(true);
    else setError("Hint: it’s the day our love born 💖");
  };

  const addMemory = async () => {
    if (!text) return;
    await addDoc(collection(db, "memories"), { text, images });
    setText("");
    setImages([]);
  };

  const deleteMemory = async (id) => {
    await deleteDoc(doc(db, "memories", id));
  };

  const handleImages = (files) => {
    const readers = Array.from(files).map(file => new Promise(res => {
      const r = new FileReader();
      r.onloadend = () => res(r.result);
      r.readAsDataURL(file);
    }));
    Promise.all(readers).then(setImages);
  };

  if (!authorized) {
    return (
      <div style={{ height: "100vh", display: "flex", justifyContent: "center", alignItems: "center", background: "linear-gradient(135deg,#ff9a9e,#fad0c4)" }}>
        <div style={{ background: "rgba(255,255,255,0.7)", backdropFilter: "blur(10px)", padding: "40px", borderRadius: "25px", textAlign: "center", boxShadow: "0 10px 40px rgba(0,0,0,0.2)" }}>
          <h2 style={{ fontSize: "24px", marginBottom: "15px" }}>Our Love Space 💕</h2>
          <input type="password" value={password} onChange={(e)=>setPassword(e.target.value)} style={{ padding: "10px", borderRadius: "10px", border: "none", width: "200px" }} />
          <br/><br/>
          <button onClick={handleLogin} style={{ background: "#ff4d6d", color: "white", padding: "10px 20px", borderRadius: "20px", border: "none" }}>Enter</button>
          {error && <p style={{ marginTop: "10px" }}>{error}</p>}
        </div>
      </div>
    );
  }

  const TimeBox = ({ value, label }) => (
    <div style={{ textAlign: "center", background: "rgba(255,255,255,0.6)", padding: "10px 15px", borderRadius: "15px", backdropFilter: "blur(5px)", boxShadow: "0 5px 15px rgba(0,0,0,0.1)" }}>
      <div style={{ fontSize: "22px", fontWeight: "bold" }}>{String(value).padStart(2,'0')}</div>
      <div style={{ fontSize: "11px" }}>{label}</div>
    </div>
  );

  return (
    <div style={{ minHeight: "100vh", padding: "20px", position: "relative", overflow: "hidden",
      background: "radial-gradient(circle at 20% 30%, #ff6a88 0%, transparent 40%), radial-gradient(circle at 80% 70%, #ff99ac 0%, transparent 40%), linear-gradient(135deg,#ff758c,#ff7eb3,#ff9a9e)"
    }}>

      {/* floating hearts */}
      {[...Array(10)].map((_,i)=> (
        <motion.div
          key={i}
          initial={{ y: "100vh", x: Math.random()*window.innerWidth, opacity: 0.3 }}
          animate={{ y: "-10vh" }}
          transition={{ duration: 8 + Math.random()*5, repeat: Infinity }}
          style={{ position: "absolute", fontSize: "20px", pointerEvents: "none" }}
        >
          💖
        </motion.div>
      ))}
      <div style={{ maxWidth: "700px", margin: "auto" }}>

        <h2 style={{ textAlign: "center", fontSize: "22px", marginBottom: "10px" }}>Toka, my love You said it and my life started</h2>

        <div style={{ display: "flex", justifyContent: "center", gap: "10px", margin: "15px 0" }}>
          <TimeBox value={time.days} label="Days" />
          <TimeBox value={time.hours} label="Hours" />
          <TimeBox value={time.minutes} label="Minutes" />
          <TimeBox value={time.seconds} label="Seconds" />
        </div>

        <h1 style={{ textAlign: "center", marginBottom: "25px", fontSize: "34px", fontWeight: "bold" }}>Welcome to our universe TA2TO2A 💖</h1>

        <div style={{ background: "rgba(255,255,255,0.7)", backdropFilter: "blur(10px)", padding: "20px", borderRadius: "25px", marginBottom: "25px", boxShadow: "0 10px 30px rgba(0,0,0,0.15)" }}>
          <textarea value={text} onChange={(e)=>setText(e.target.value)} placeholder="Write memory" style={{ width: "100%", padding: "10px", borderRadius: "10px", border: "none", marginBottom: "10px" }} />
          <input type="file" multiple onChange={(e)=>handleImages(e.target.files)} />

          <div style={{ display: "flex", gap: "5px", marginTop: "10px" }}>
            {images.map((img,i)=>(<img key={i} src={img} style={{ width: "60px", borderRadius: "10px" }} />))}
          </div>

          <button onClick={addMemory} style={{ marginTop: "10px", background: "#ff4d6d", color: "white", padding: "10px 15px", borderRadius: "20px", border: "none" }}>Save Memory</button>
        </div>

        {memories.map(m => (
          <div key={m.id} style={{ background: "rgba(255,255,255,0.7)", backdropFilter: "blur(10px)", padding: "20px", borderRadius: "25px", marginBottom: "20px", boxShadow: "0 10px 30px rgba(0,0,0,0.15)" }}>
            <p style={{ marginBottom: "10px" }}>{m.text}</p>
            {m.images && <ImageCarousel images={m.images} />}
            <button onClick={()=>deleteMemory(m.id)} style={{ color: "#ff4d6d", border: "none", background: "none" }}>Delete</button>
          </div>
        ))}

      </div>
    </div>
  );
}


