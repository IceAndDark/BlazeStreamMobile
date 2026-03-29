# BlazeStreamMobile
onscreen unmute

```
(() => {
    if (document.getElementById('blaze-unmuter-icon')) return;

    const btn = document.createElement('button');
    btn.id = 'blaze-unmuter-icon';
    btn.innerHTML = '🔊'; // Only using the symbol
    
    Object.assign(btn.style, {
        position: 'fixed',
        top: '15px',
        left: '15px',
        zIndex: '2147483647', // Maximum possible z-index
        width: '50px',
        height: '50px',
        fontSize: '24px',
        backgroundColor: '#673AB7', 
        color: 'white',
        border: '2px solid rgba(255,255,255,0.4)',
        borderRadius: '12px',
        boxShadow: '0 4px 12px rgba(0,0,0,0.4)',
        cursor: 'pointer',
        display: 'flex',
        alignItems: 'center',
        justifyContent: 'center',
        transition: 'transform 0.1s active'
    });

    btn.onclick = () => {
        const videos = document.querySelectorAll('video');
        
        if (videos.length === 0) {
            btn.innerHTML = '❓';
            btn.style.backgroundColor = '#555';
            setTimeout(() => {
                btn.innerHTML = '🔊';
                btn.style.backgroundColor = '#673AB7';
            }, 1000);
            return;
        }

        videos.forEach(v => {
            v.muted = false;
            v.volume = 1.0;
            v.play().catch(() => {}); 
        });

        // Visual feedback
        btn.innerHTML = '✅';
        btn.style.backgroundColor = '#4CAF50';
        setTimeout(() => {
            btn.innerHTML = '🔊';
            btn.style.backgroundColor = '#673AB7';
        }, 1000);
    };

    document.body.appendChild(btn);
    console.log('✅ Symbol-only unmuter loaded top-left');
})();
