# saloon-
GENTS SALOON SELL ALL DETAILS IN OUR WEBSITE
import React, { useState } from 'react';
import { motion } from 'framer-motion';
import { MapPin, Calendar, Star, Phone, ChevronRight } from 'lucide-react';

const GautamGentsParlour = () => {
  const [language, setLanguage] = useState('en');

  const services = [
    { id: 1, name: 'Fade Cut', nameHi: 'फ़ेड कट', price: '₹200', duration: '30 min', icon: '✂️' },
    { id: 2, name: 'Beard Grooming', nameHi: 'दाढ़ी ग्रूमिंग', price: '₹150', duration: '20 min', icon: '🧔' },
    { id: 3, name: 'Groom Package', nameHi: 'दूल्हा पैकेज', price: '₹1500+', duration: '120 min', icon: '👑' },
  ];

  const content = {
    en: { title: "Gautam Gents Parlour", sub: "Mastering the Art of Grooming", book: "Book Appointment", address: "Mannaka Rd, Alwar" },
    hi: { title: "गौतम जेंट्स पार्लर", sub: "ग्रूमिंग की कला में महारत", book: "अपॉइंटमेंट बुक करें", address: "मन्नाका रोड, अलवर" }
  };

  const t = content[language];

  return (
    <div className="min-h-screen bg-[#0a0a0a] text-gray-100 font-sans selection:bg-gold-500">
      {/* --- Navigation --- */}
      <nav className="flex justify-between items-center p-6 border-b border-yellow-600/20 backdrop-blur-md sticky top-0 z-50">
        <h1 className="text-2xl font-bold tracking-tighter text-transparent bg-clip-text bg-gradient-to-r from-yellow-400 to-yellow-700">
          GAUTAM GENTS
        </h1>
        <div className="flex gap-4 items-center">
          <button onClick={() => setLanguage(language === 'en' ? 'hi' : 'en')} className="text-xs border border-yellow-600/50 px-2 py-1 rounded hover:bg-yellow-600/10 transition">
            {language === 'en' ? 'हिंदी' : 'English'}
          </button>
          <button className="bg-yellow-600 hover:bg-yellow-500 text-black px-4 py-2 rounded-full font-bold text-sm transition-transform active:scale-95">
            {t.book}
          </button>
        </div>
      </nav>

      {/* --- Hero Section --- */}
      <header className="relative h-[70vh] flex items-center justify-center overflow-hidden">
        <div className="absolute inset-0 z-0 bg-[url('https://images.unsplash.com/photo-1503951914875-452162b0f3f1?q=80&w=2070')] bg-cover bg-center opacity-30 grayscale" />
        <div className="absolute inset-0 bg-gradient-to-b from-transparent to-[#0a0a0a]" />
        
        <motion.div 
          initial={{ opacity: 0, y: 30 }}
          animate={{ opacity: 1, y: 0 }}
          className="relative z-10 text-center px-4"
        >
          <div className="flex justify-center mb-4">
            {[1,2,3,4,5].map(s => <Star key={s} size={18} className="fill-yellow-500 text-yellow-500" />)}
          </div>
          <h2 className="text-5xl md:text-7xl font-black mb-4 uppercase italic tracking-tight">{t.title}</h2>
          <p className="text-xl text-yellow-500/80 mb-8 font-light tracking-widest">{t.sub}</p>
        </motion.div>
      </header>

      {/* --- 3D-ish Service Cards --- */}
      <section className="max-w-6xl mx-auto py-20 px-6">
        <h3 className="text-3xl font-bold mb-12 border-l-4 border-yellow-600 pl-4 uppercase">Our Services</h3>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
          {services.map((service) => (
            <motion.div 
              key={service.id}
              whileHover={{ rotateY: 10, rotateX: -5, scale: 1.02 }}
              className="bg-zinc-900 border border-white/5 p-8 rounded-2xl relative overflow-hidden group cursor-pointer"
            >
              <div className="absolute top-0 right-0 p-4 opacity-10 group-hover:opacity-30 text-5xl transition-opacity">
                {service.icon}
              </div>
              <h4 className="text-2xl font-bold mb-2">{language === 'en' ? service.name : service.nameHi}</h4>
              <p className="text-yellow-600 font-mono text-lg mb-4">{service.price}</p>
              <div className="flex items-center text-gray-500 text-sm">
                <Calendar size={14} className="mr-2" /> {service.duration}
              </div>
              <div className="mt-6 flex items-center text-xs font-bold text-yellow-500 group-hover:translate-x-2 transition-transform">
                BOOK NOW <ChevronRight size={14} />
              </div>
            </motion.div>
          ))}
        </div>
      </section>

      {/* --- Floating Location FAB --- */}
      <motion.a 
        href="https://goo.gl/maps/..." // Replace with actual Google Maps link
        target="_blank"
        whileHover={{ scale: 1.1 }}
        className="fixed bottom-8 right-8 bg-yellow-600 p-4 rounded-full shadow-2xl shadow-yellow-600/20 z-50 cursor-pointer"
      >
        <MapPin className="text-black" size={28} />
      </motion.a>
    </div>
  );
};

export default GautamGentsParlour;
import React, { useState } from 'react';
import { motion, AnimatePresence } from 'framer-motion';
import { CheckCircle, Clock, User, Scissors, CreditCard } from 'lucide-react';

const BookingWizard = () => {
  const [step, setStep] = useState(1);
  const [bookingData, setBookingData] = useState({
    service: '',
    barber: '',
    time: '',
    userType: 'Regular', // Default
    payment: 'UPI'
  });

  const barbers = [
    { id: 'b1', name: 'Rahul (Senior)', role: 'Master Stylist', rating: 5.0 },
    { id: 'b2', name: 'Amit', role: 'Fade Specialist', rating: 4.8 },
    { id: 'b3', name: 'Suresh', role: 'Beard Expert', rating: 4.9 }
  ];

  const timeSlots = ["10:00 AM", "11:30 AM", "02:00 PM", "04:30 PM", "07:00 PM"];

  const nextStep = () => setStep(s => s + 1);
  const prevStep = () => setStep(s => s - 1);

  return (
    <div className="max-w-2xl mx-auto p-6 bg-zinc-950 border border-yellow-600/30 rounded-3xl shadow-2xl mt-10">
      {/* --- Progress Header --- */}
      <div className="flex justify-between mb-10 px-4">
        {[1, 2, 3, 4].map((num) => (
          <div key={num} className={`h-1 w-full mx-1 rounded-full ${step >= num ? 'bg-yellow-600' : 'bg-zinc-800'}`} />
        ))}
      </div>

      <AnimatePresence mode="wait">
        {/* STEP 1: SELECT BARBER */}
        {step === 1 && (
          <motion.div 
            initial={{ x: 20, opacity: 0 }} animate={{ x: 0, opacity: 1 }} exit={{ x: -20, opacity: 0 }}
            className="space-y-4"
          >
            <h2 className="text-2xl font-bold flex items-center gap-2"><User className="text-yellow-600"/> Choose your Barber</h2>
            <div className="grid gap-4">
              {barbers.map(b => (
                <button 
                  key={b.id}
                  onClick={() => { setBookingData({...bookingData, barber: b.name}); nextStep(); }}
                  className={`p-4 rounded-xl border flex justify-between items-center transition-all ${bookingData.barber === b.name ? 'border-yellow-600 bg-yellow-600/10' : 'border-zinc-800 hover:border-zinc-600'}`}
                >
                  <div className="text-left">
                    <p className="font-bold">{b.name}</p>
                    <p className="text-xs text-zinc-500">{b.role}</p>
                  </div>
                  <span className="text-yellow-500 text-sm">★ {b.rating}</span>
                </button>
              ))}
            </div>
          </motion.div>
        )}

        {/* STEP 2: SELECT TIME */}
        {step === 2 && (
          <motion.div 
            initial={{ x: 20, opacity: 0 }} animate={{ x: 0, opacity: 1 }} exit={{ x: -20, opacity: 0 }}
            className="space-y-4"
          >
            <h2 className="text-2xl font-bold flex items-center gap-2"><Clock className="text-yellow-600"/> Select Time Slot</h2>
            <div className="grid grid-cols-2 gap-3">
              {timeSlots.map(slot => (
                <button 
                  key={slot}
                  onClick={() => { setBookingData({...bookingData, time: slot}); nextStep(); }}
                  className="p-3 bg-zinc-900 rounded-lg hover:bg-yellow-600 hover:text-black transition-colors font-mono"
                >
                  {slot}
                </button>
              ))}
            </div>
            <button onClick={prevStep} className="text-zinc-500 text-sm underline mt-4">Back</button>
          </motion.div>
        )}

        {/* STEP 3: USER TYPE & LOYALTY */}
        {step === 3 && (
          <motion.div 
            initial={{ x: 20, opacity: 0 }} animate={{ x: 0, opacity: 1 }} exit={{ x: -20, opacity: 0 }}
            className="space-y-4"
          >
            <h2 className="text-2xl font-bold italic">User Category</h2>
            <div className="flex gap-2">
              {['New Customer', 'Regular', 'VIP'].map(type => (
                <button 
                  key={type}
                  onClick={() => setBookingData({...bookingData, userType: type})}
                  className={`flex-1 py-3 rounded-md text-xs font-bold uppercase tracking-widest transition-all ${bookingData.userType === type ? 'bg-yellow-600 text-black' : 'bg-zinc-900 border border-zinc-700 text-zinc-400'}`}
                >
                  {type}
                </button>
              ))}
            </div>
            <div className="p-4 bg-zinc-900 rounded-xl border border-zinc-800 mt-6">
              <p className="text-sm text-zinc-400">Review Selection:</p>
              <p className="text-yellow-600 font-bold">{bookingData.barber} at {bookingData.time}</p>
            </div>
            <button onClick={nextStep} className="w-full py-4 bg-white text-black font-black uppercase rounded-full hover:bg-yellow-500">Proceed to Payment</button>
          </motion.div>
        )}

        {/* STEP 4: PAYMENT SELECTION */}
        {step === 4 && (
          <motion.div 
            initial={{ scale: 0.9, opacity: 0 }} animate={{ scale: 1, opacity: 1 }}
            className="text-center space-y-6"
          >
            <h2 className="text-2xl font-bold uppercase tracking-tighter">Final Step</h2>
            <div className="bg-white p-6 rounded-2xl mx-auto w-48 h-48 flex flex-col items-center justify-center">
               <div className="bg-zinc-200 w-32 h-32 mb-2 flex items-center justify-center text-black text-[10px] text-center">
                  [DYNAMIC QR CODE FOR UPI]
               </div>
               <p className="text-[10px] text-zinc-500 font-bold">SCAN TO PAY ₹500</p>
            </div>
            <div className="flex gap-4">
              <button className="flex-1 py-3 border border-zinc-700 rounded-lg text-sm">Cash on Delivery</button>
              <button className="flex-1 py-3 bg-yellow-600 text-black font-bold rounded-lg text-sm">Pay Online</button>
            </div>
          </motion.div>
        )}
      </AnimatePresence>
    </div>
  );
};

export default BookingWizard;
from pydantic import BaseModel, Field
from typing import Optional, List
from datetime import datetime

class Appointment(BaseModel):
    customer_name: str
    phone: str
    service_id: str
    barber_id: str
    appointment_time: str  # e.g., "2026-02-21 14:00"
    user_type: str = "Regular" # Regular, VIP, New
    payment_status: str = "Pending" # Pending, Paid, COD
    total_price: float
    
class Barber(BaseModel):
    name: str
    specialty: List[str]
    is_available: bool = True
    rating: float = 5.0
    from fastapi import FastAPI, HTTPException
from motor.motor_asyncio import AsyncIOMotorClient
from fastapi.middleware.cors import CORSMiddleware
import os

app = FastAPI(title="Gautam Gents Parlour API")

# Enable CORS for our React Frontend
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"],
)

# MongoDB Connection
MONGO_URL = "mongodb://localhost:27017" # Update for production
client = AsyncIOMotorClient(MONGO_URL)
db = client.gautam_parlour

@app.post("/api/bookings")
async def create_booking(booking: Appointment):
    # 1. Check for double-booking
    existing = await db.appointments.find_one({
        "barber_id": booking.barber_id,
        "appointment_time": booking.appointment_time
    })
    
    if existing:
        raise HTTPException(status_code=400, detail="Barber already booked for this slot!")

    # 2. Insert into MongoDB
    new_booking = await db.appointments.insert_one(booking.dict())
    
    # 3. Handle User Type Logic (Example: VIP logging)
    if booking.user_type == "VIP":
        print(f"Priority Alert: VIP Booking confirmed for {booking.customer_name}")

    return {"status": "success", "booking_id": str(new_booking.inserted_id)}

@app.get("/api/barbers")
async def get_barbers():
    barbers = await db.barbers.find().to_list(100)
    return barbers
    def generate_booking_message(data):
    """
    Generates a bilingual message (Hindi & English) 
    tailored to the user type (VIP, New, or Regular).
    """
    customer = data['customer_name']
    time = data['appointment_time']
    barber = data['barber_name']
    user_type = data['user_type']
    
    # VIP Special Greeting
    vip_tag = "⭐ VIP PRIORITY | " if user_type == "VIP" else ""
    
    message = (
        f"{vip_tag}Namaste {customer}!\n"
        f"Your appointment at Gautam Gents Parlour is CONFIRMED.\n"
        f"📅 Time: {time}\n"
        f"✂️ Barber: {barber}\n"
        f"📍 Location: Mannaka Rd, Alwar.\n\n"
        f"नमस्ते {customer}!\n"
        f"गौतम जेंट्स पार्लर में आपका अपॉइंटमेंट कन्फर्म हो गया है।\n"
        f"समय: {time}\n"
        f"धन्यवाद!"
    )
    return message
    const handleWhatsAppBooking = () => {
  const phoneNumber = "91XXXXXXXXXX"; // Put your Alwar shop number here
  const message = `Namaste! I want to book:
  Service: ${bookingData.service}
  Barber: ${bookingData.barber}
  Time: ${bookingData.time}
  User Type: ${bookingData.userType}`;
  
  const encodedMessage = encodeURIComponent(message);
  window.open(`https://wa.me/${phoneNumber}?text=${encodedMessage}`, '_blank');
};
