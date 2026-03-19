<script setup>
</script>

<template>
    <section class="collection-section">
        <div class="collection-container">
            <div class="collection-image">
                <img src="../../assets/banner-large.png" alt="Colección Siluetas Nocturnas">
            </div>
            
            <div class="collection-overlay">
                <div class="collection-content">
                    <span class="collection-tag">Nueva Colección</span>
                    <h2>Siluetas Nocturnas</h2>
                    <p>Una oda a la forma y la textura en su expresión más pura. 
                        Descubre una colección que juega con las sombras y la luz 
                        donde cada pieza cuenta una historia de elegancia y misterio.
                    </p>
                    <a href="#" class="btn-collection">Ver Colección</a>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
.collection-section {
    padding: 40px 5%;
    max-width: 1400px;
    margin: 0 auto;
}

.collection-container {
    position: relative;
    width: 100%;
    aspect-ratio: 16/9;
    max-height: 600px;
    overflow: hidden;
}

.collection-image {
    width: 100%;
    height: 100%;
}

.collection-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.collection-container:hover .collection-image img {
    transform: scale(1.03);
}

.collection-overlay {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    padding: 60px;
    background: linear-gradient(
        90deg, 
        rgba(0, 0, 0, 0.05) 0%, 
        rgba(0, 0, 0, 0.2) 50%, 
        rgba(0, 0, 0, 0.5) 100%
    );
}

.collection-content {
    max-width: 480px;
    color: #fff;
}

.collection-tag {
    display: inline-block;
    font-size: 0.65rem;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: rgba(255, 255, 255, 0.7);
    margin-bottom: 16px;
    padding-bottom: 8px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.3);
}

.collection-content h2 {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(2rem, 5vw, 3.5rem);
    font-weight: 300;
    font-style: italic;
    letter-spacing: 0.1em;
    margin: 0 0 24px;
    line-height: 1.2;
}

.collection-content p {
    font-size: 0.95rem;
    line-height: 1.7;
    color: rgba(255, 255, 255, 0.85);
    margin: 0 0 32px;
    font-weight: 300;
}

.btn-collection {
    display: inline-block;
    padding: 14px 36px;
    background: transparent;
    border: 1px solid rgba(255, 255, 255, 0.6);
    color: #fff;
    font-size: 0.7rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    text-decoration: none;
    transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    overflow: hidden;
}

.btn-collection::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: #fff;
    transition: left 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    z-index: -1;
}

.btn-collection:hover {
    border-color: #fff;
    color: #000;
}

.btn-collection:hover::before {
    left: 0;
}

/* Responsive */
@media (max-width: 768px) {
    .collection-overlay {
        padding: 30px;
        justify-content: center;
        text-align: center;
        background: linear-gradient(
            180deg, 
            rgba(0, 0, 0, 0.4) 0%, 
            rgba(0, 0, 0, 0.5) 100%
        );
    }
    
    .collection-content {
        max-width: 100%;
    }
    
    .collection-container {
        aspect-ratio: 4/5;
    }
    
    .collection-content p {
        font-size: 0.85rem;
    }
}
</style>
