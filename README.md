# careerthinker
import React, { useState } from 'react';
import { PageTab, FeatureTab } from './types';
import { Navbar } from './components/Navbar';
import { Footer } from './components/Footer';
import { Hero } from './components/home/Hero';
import { FeaturesGrid } from './components/home/FeaturesGrid';
import { HowItWorks } from './components/home/HowItWorks';
import { Testimonials } from './components/home/Testimonials';
import { FAQ } from './components/home/FAQ';
import { AboutPage } from './components/about/AboutPage';
import { FeaturesPage } from './components/features/FeaturesPage';
import { ContactPage } from './components/contact/ContactPage';
import { ConsultationModal } from './components/ConsultationModal';

export default function App() {
  const [activeTab, setActiveTab] = useState<PageTab>('home');
  const [selectedFeature, setSelectedFeature] = useState<FeatureTab>('guidance');
  const [isConsultationOpen, setIsConsultationOpen] = useState(false);

  const handleSelectFeature = (feature: FeatureTab) => {
    setSelectedFeature(feature);
    setActiveTab('features');
    window.scrollTo({ top: 0, behavior: 'smooth' });
  };

  return (
    <div className="min-h-screen bg-slate-50 text-slate-900 font-sans flex flex-col selection:bg-blue-100 selection:text-blue-900">
      
      {/* Navigation Bar */}
      <Navbar
        activeTab={activeTab}
        setActiveTab={setActiveTab}
        onOpenConsultation={() => setIsConsultationOpen(true)}
      />

      {/* Main Page View Content */}
      <main className="flex-1">
        {activeTab === 'home' && (
          <div className="animate-in fade-in duration-300">
            <Hero
              setActiveTab={setActiveTab}
              onOpenConsultation={() => setIsConsultationOpen(true)}
            />
            <FeaturesGrid
              setActiveTab={setActiveTab}
              onSelectFeature={handleSelectFeature}
            />
            <HowItWorks setActiveTab={setActiveTab} />
            <Testimonials />
            <FAQ />
          </div>
        )}

        {activeTab === 'about' && (
          <div className="animate-in fade-in duration-300">
            <AboutPage
              setActiveTab={setActiveTab}
              onOpenConsultation={() => setIsConsultationOpen(true)}
            />
          </div>
        )}

        {activeTab === 'features' && (
          <div className="animate-in fade-in duration-300">
            <FeaturesPage initialFeature={selectedFeature} />
          </div>
        )}

        {activeTab === 'contact' && (
          <div className="animate-in fade-in duration-300">
            <ContactPage onOpenConsultation={() => setIsConsultationOpen(true)} />
          </div>
        )}
      </main>

      {/* Footer */}
      <Footer setActiveTab={setActiveTab} />

      {/* Booking Modal */}
      <ConsultationModal
        isOpen={isConsultationOpen}
        onClose={() => setIsConsultationOpen(false)}
      />

    </div>
  );
}
