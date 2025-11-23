# Assignment-Test-for-Junior-Engineer---Gatot-Arifianto
Assignment Test - Gator Arifianto
import React, { useState, useEffect } from 'react';
// Asumsi Tailwind CSS tersedia di lingkungan React Native/Web.
// Menggunakan lucide-react untuk ikon.

// Ikon sederhana (Simulasi Lucide Icons)
const Clock = (props) => <svg {...props} xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>;
const Zap = (props) => <svg {...props} xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"/></svg>;
const Server = (props) => <svg {...props} xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><rect x="2" y="2" width="20" height="8" rx="2" ry="2"/><rect x="2" y="14" width="20" height="8" rx="2" ry="2"/><line x1="6" y1="6" x2="6.01" y2="6"/><line x1="6" y1="18" x2="6.01" y2="18"/></svg>;
const Bot = (props) => <svg {...props} xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="M12 8V4"/><path d="M10 2h4"/><path d="M10 22h4"/><path d="M12 16v6"/><path d="M12 12h.01"/><rect x="2" y="8" width="20" height="4" rx="1"/><rect x="2" y="12" width="20" height="4" rx="1"/></svg>;
const Upload = (props) => <svg {...props} xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="17 8 12 3 7 8"/><line x1="12" y1="3" x2="12" y2="15"/></svg>;
const PenTool = (props) => <svg {...props} xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="M12 19l7-7 3 3-7 7-3-3z"/><path d="M18 13l-1.5-1.5"/></svg>;
const CheckCircle = (props) => <svg {...props} xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg>;
const XCircle = (props) => <svg {...props} xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"><circle cx="12" cy="12" r="10"/><line x1="15" y1="9" x2="9" y2="15"/><line x1="9" y1="9" x2="15" y2="15"/></svg>;


// --- Komponen Utama Aplikasi ---
const App = () => {
    // Simulasi status real-time dari Agen Backend
    const [systemStatus, setSystemStatus] = useState({
        overall: 'AKTIF & TERJADWAL',
        lastExecution: '2025-11-23 11:00:00 WIB',
        nextExecution: '2025-11-23 13:00:00 WIB',
        executionInterval: '2 Jam',
    });

    const [agentStatuses, setAgentStatuses] = useState([
        {
            name: 'Agen Scraping Data',
            description: 'Mengambil data hotel di Tangerang Kota dari Google Search.',
            status: 'BERHASIL',
            icon: Server,
            color: 'green',
            lastRun: '11:00:05 WIB',
            metrics: '25 Data Hotel Baru Ditemukan',
            methodology: 'Spec Driven Development (SDD) untuk keandalan data.',
        },
        {
            name: 'Agen Generasi Konten',
            description: 'Menciptakan teks blog dan aset gambar/visual unik.',
            status: 'BERHASIL',
            icon: PenTool,
            color: 'green',
            lastRun: '11:05:40 WIB',
            metrics: '3 Blog & 6 Gambar (3:4 untuk IG, 9:16 untuk TikTok) Dihasilkan',
            methodology: 'AI Vibe Coding untuk daya tarik konten.',
        },
        {
            name: 'Agen Publikasi Multi-Platform',
            description: 'Otomatisasi posting ke Lynx/RN App, Instagram, & TikTok.',
            status: 'BERHASIL',
            icon: Upload,
            color: 'green',
            lastRun: '11:08:15 WIB',
            metrics: '3 Publikasi Berhasil (Lynx, IG, TikTok).',
            methodology: 'SDD untuk integrasi API dan kepatuhan jadwal.',
        },
    ]);

    const [configuration, setConfiguration] = useState({
        location: 'Tangerang Kota',
        vibe: 'Modern & Eksploratif',
        imageGenerator: 'DALL-E 3 / Gemini-Image',
        socialTargets: ['Instagram', 'TikTok', 'Lynx/RN App'],
    });

    // useEffect untuk menyimulasikan pembaruan waktu berjalan
    useEffect(() => {
        const interval = setInterval(() => {
            // Simulasi waktu real-time
            setSystemStatus(prev => ({
                ...prev,
                lastExecution: new Date().toLocaleTimeString('id-ID', { hour: '2-digit', minute: '2-digit', second: '2-digit' }) + ' WIB (Contoh)',
            }));
        }, 60000); // Update setiap menit

        return () => clearInterval(interval);
    }, []);

    const getStatusIndicator = (status) => {
        if (status === 'BERHASIL') return <CheckCircle className="w-5 h-5 text-emerald-500" />;
        if (status === 'GAGAL') return <XCircle className="w-5 h-5 text-red-500" />;
        return <Zap className="w-5 h-5 text-yellow-500 animate-pulse" />;
    };

    const getStatusColor = (status) => {
        if (status === 'BERHASIL') return 'bg-emerald-500';
        if (status === 'GAGAL') return 'bg-red-500';
        return 'bg-yellow-500';
    };

    const AgentCard = ({ agent }) => (
        <div className="bg-white p-6 rounded-xl shadow-lg border border-slate-200 hover:shadow-xl transition-shadow duration-300">
            <div className="flex items-start justify-between">
                <div className="flex items-center">
                    <agent.icon className={`w-8 h-8 text-sky-600 p-1.5 rounded-full ${getStatusColor(agent.status).replace('bg', 'bg-opacity-10 text')}`} />
                    <h3 className="text-xl font-semibold text-slate-800 ml-3">{agent.name}</h3>
                </div>
                <div className={`px-3 py-1 text-xs font-bold text-white rounded-full ${getStatusColor(agent.status)}`}>
                    {agent.status}
                </div>
            </div>
            
            <p className="text-slate-600 mt-3 text-sm">{agent.description}</p>
            
            <div className="mt-4 pt-4 border-t border-slate-100 space-y-2">
                <div className="flex justify-between text-sm text-slate-700">
                    <span className="font-medium">Jalankan Terakhir:</span>
                    <span>{agent.lastRun}</span>
                </div>
                <div className="text-sm text-slate-700">
                    <span className="font-medium block mb-1">Metrik Utama:</span>
                    <p className="text-xs text-slate-500 italic">{agent.metrics}</p>
                </div>
                <div className="text-sm text-slate-700">
                    <span className="font-medium block mb-1">Metodologi:</span>
                    <p className="text-xs text-sky-600 italic font-medium">{agent.methodology}</p>
                </div>
            </div>
        </div>
    );

    return (
        <div className="min-h-screen bg-slate-50 p-4 md:p-8">
            <header className="mb-8 max-w-7xl mx-auto">
                <h1 className="text-3xl font-extrabold text-slate-900">
                    Dashboard Agen Konten AI
                </h1>
                <p className="text-xl text-sky-600 mt-1">
                    Pengawasan Sistem Otomatisasi Hotel Tangerang
                </p>
            </header>

            <main className="max-w-7xl mx-auto space-y-8">
                
                {/* 1. Status Utama Sistem */}
                <div className="bg-white p-6 rounded-xl shadow-xl border-t-4 border-sky-500">
                    <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
                        <StatusBox title="Status Keseluruhan" value={systemStatus.overall} icon={Bot} color="text-sky-600" />
                        <StatusBox title="Interval Eksekusi" value={systemStatus.executionInterval} icon={Clock} color="text-indigo-600" />
                        <StatusBox title="Jalankan Terakhir (WIB)" value={systemStatus.lastExecution} icon={Zap} color="text-emerald-600" />
                        <StatusBox title="Jalankan Berikutnya" value={systemStatus.nextExecution} icon={Zap} color="text-yellow-600" />
                    </div>
                </div>

                {/* 2. Status Agen Individu */}
                <h2 className="text-2xl font-bold text-slate-800 pt-4">Status Siklus Otomatisasi</h2>
                <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
                    {agentStatuses.map((agent, index) => (
                        <AgentCard key={index} agent={agent} />
                    ))}
                </div>

                {/* 3. Konfigurasi Proyek (Settings) */}
                <div className="bg-white p-6 rounded-xl shadow-lg border border-slate-200">
                    <h2 className="text-2xl font-bold text-slate-800 flex items-center mb-4">
                        <Server className="w-6 h-6 mr-2 text-sky-500"/> Konfigurasi Agen (Spec Driven Development)
                    </h2>
                    <p className="text-slate-600 mb-4 text-sm">
                        Pengaturan ini mendefinisikan batasan keras (*hard limits*) dan format output yang harus dipatuhi oleh Agen AI.
                    </p>
                    <div className="grid grid-cols-1 md:grid-cols-3 gap-4 text-slate-700">
                        <ConfigItem title="Target Lokasi Scrape" value={configuration.location} description="Wajib dipatuhi: Tangerang Kota (Berdasarkan parameter Google Search/API)." />
                        <ConfigItem title="Gaya Konten (Vibe Coding)" value={configuration.vibe} description="Gaya konten yang dihasilkan oleh model AI (digunakan oleh Agen Generasi)." />
                        <ConfigItem title="Platform Publikasi Wajib" value={configuration.socialTargets.join(', ')} description="Output wajib yang dipublikasikan setiap 2 jam." />
                    </div>
                </div>

                {/* 4. Log Terbaru (Placeholder) */}
                <div className="bg-white p-6 rounded-xl shadow-lg border border-slate-200">
                    <h2 className="text-2xl font-bold text-slate-800 mb-4">Log Eksekusi Terbaru</h2>
                    <LogTable />
                </div>

            </main>

            <footer className="mt-8 text-center text-slate-500 text-sm p-4">
                &copy; {new Date().getFullYear()} Agen AI Konten | Ditenagai oleh Lynx/RN App Interface.
            </footer>
        </div>
    );
};

// Komponen Pembantu: Status Box
const StatusBox = ({ title, value, icon: Icon, color }) => (
    <div className="p-3 rounded-lg bg-slate-50 border border-slate-200">
        <div className="flex items-center">
            <Icon className={`w-5 h-5 ${color}`} />
            <span className="text-xs font-medium text-slate-500 ml-2">{title}</span>
        </div>
        <p className="text-lg font-bold text-slate-800 mt-1">{value}</p>
    </div>
);

// Komponen Pembantu: Config Item
const ConfigItem = ({ title, value, description }) => (
    <div className="p-3 bg-slate-50 rounded-lg border border-slate-200">
        <p className="text-sm font-semibold text-sky-700">{title}</p>
        <p className="text-lg font-bold text-slate-900 mt-1">{value}</p>
        <p className="text-xs text-slate-500 mt-1">{description}</p>
    </div>
);

// Komponen Pembantu: Log Table
const LogTable = () => {
    const logs = [
        { time: '11:08:15', agent: 'Publikasi', status: 'BERHASIL', detail: 'Posting IG & TikTok Selesai. Tautan: [Tautan Log]', type: 'Success' },
        { time: '11:05:40', agent: 'Generasi', status: 'BERHASIL', detail: '3 Konten dan Aset Gambar Dihasilkan. Vibe: Eksploratif', type: 'Success' },
        { time: '11:00:05', agent: 'Scraping', status: 'BERHASIL', detail: 'Scraping Tangerang Kota Selesai. 25 entri baru.', type: 'Success' },
        { time: '09:08:20', agent: 'Publikasi', status: 'GAGAL', detail: 'Gagal Posting TikTok (Autentikasi Kedaluwarsa).', type: 'Error' },
        { time: '09:05:30', agent: 'Generasi', status: 'BERHASIL', detail: '3 Konten Dihasilkan.', type: 'Success' },
    ];

    const getRowStyle = (type) => {
        if (type === 'Success') return 'bg-emerald-50 text-emerald-800';
        if (type === 'Error') return 'bg-red-50 text-red-800';
        return 'bg-slate-50 text-slate-700';
    };

    return (
        <div className="overflow-x-auto rounded-lg border border-slate-200">
            <table className="min-w-full divide-y divide-slate-200">
                <thead className="bg-slate-50">
                    <tr>
                        <th className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Waktu (WIB)</th>
                        <th className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Agen</th>
                        <th className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Status</th>
                        <th className="px-6 py-3 text-left text-xs font-medium text-slate-500 uppercase tracking-wider">Detail Log</th>
                    </tr>
                </thead>
                <tbody className="divide-y divide-slate-100">
                    {logs.map((log, index) => (
                        <tr key={index} className={getRowStyle(log.type)}>
                            <td className="px-6 py-4 whitespace-nowrap text-sm font-medium">{log.time}</td>
                            <td className="px-6 py-4 whitespace-nowrap text-sm">{log.agent}</td>
                            <td className="px-6 py-4 whitespace-nowrap text-sm font-semibold">{log.status}</td>
                            <td className="px-6 py-4 text-sm">{log.detail}</td>
                        </tr>
                    ))}
                </tbody>
            </table>
        </div>
    );
};

export default App;
