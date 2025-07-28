---
layout: default
title: /vibes
permalink: /vibes/
---

<div id="vibes-container" class="vibes-container">
  <div id="loading" class="loading">
    <span class="blink">> loading_vibes.exe...</span>
  </div>
</div>

<div id="spotify-container" class="spotify-container">
  <h2 class="spotify-title">> recent_sounds.mp3</h2>
  <div id="spotify-tracks" class="spotify-tracks">
    <div class="spotify-loading">
      <span class="blink">loading spotify data...</span>
    </div>
  </div>
</div>

<script>
class ArenaVibes {
  constructor() {
    this.container = document.getElementById('vibes-container');
    this.loading = document.getElementById('loading');
    this.placedBlocks = [];
    this.animationDelay = 150; // Slower animation for better visual flow
  }

  async init() {
    try {
      console.log('Starting vibes page initialization...');
      const blocks = await this.fetchSampleBlocks();
      console.log('Fetched blocks:', blocks.length, blocks);
      
      this.hideLoading();
      
      if (blocks && blocks.length > 0) {
        console.log('Displaying blocks...');
        this.displayBlocks(blocks);
        // Only show API info if we successfully got blocks from API
        if (blocks[0] && blocks[0].id !== 'fallback-1') {
          console.log('Content from API, showing info');
        } else {
          console.log('Using fallback content');
        }
      } else {
        console.log('No blocks found, showing error and fallback...');
        this.showError();
        const fallbackBlocks = this.getFallbackBlocks();
        this.displayBlocks(fallbackBlocks);
      }
    } catch (error) {
      console.error('Error loading vibes:', error);
      this.showError();
      const fallbackBlocks = this.getFallbackBlocks();
      this.displayBlocks(fallbackBlocks);
    }
  }

  async fetchSampleBlocks() {
    try {
      console.log('Attempting to fetch Are.na content...');
      const blocks = await this.fetchFromMultipleSources();
      console.log('Fetched', blocks.length, 'blocks from API');
      
      if (blocks.length === 0) {
        console.log('No API content found, using fallback blocks');
        return this.getFallbackBlocks();
      }
      
      return blocks;
    } catch (error) {
      console.error('Error in fetchSampleBlocks:', error);
      return this.getFallbackBlocks();
    }
  }

  async fetchFromMultipleSources() {
    console.log('Fetching from multiple sources...');
    const allBlocks = [];
    
    // Method 1: Try specific curated public channels first (more reliable)
    const curatedChannels = [
      'arena-influences',
      'creative-coding', 
      'contemporary-art-daily',
      'ornament-for-the-everyday'
    ];

    console.log('Trying curated channels...');
    for (const channelSlug of curatedChannels) {
      try {
        console.log(`Fetching channel: ${channelSlug}`);
        const channelResponse = await fetch(`https://api.are.na/v2/channels/${channelSlug}`);
        
        if (!channelResponse.ok) {
          console.log(`Channel ${channelSlug} returned status: ${channelResponse.status}`);
          continue;
        }
        
        const channelData = await channelResponse.json();
        console.log(`Channel ${channelSlug} data:`, channelData);
        
        if (channelData.contents && channelData.contents.length > 0) {
          const visualBlocks = channelData.contents
            .filter(block => {
              return block.class === 'Image' || 
                     (block.class === 'Link' && block.image) ||
                     block.class === 'Text';
            })
            .slice(0, 4);
          
          console.log(`Adding ${visualBlocks.length} blocks from ${channelSlug}`);
          allBlocks.push(...visualBlocks);
        }
        
        await new Promise(resolve => setTimeout(resolve, 300));
        
        // Stop if we have enough content
        if (allBlocks.length >= 12) break;
        
      } catch (error) {
        console.error(`Error fetching channel ${channelSlug}:`, error);
      }
    }

    console.log(`Total blocks collected: ${allBlocks.length}`);
    
    // Shuffle and limit total blocks
    this.shuffleArray(allBlocks);
    return allBlocks.slice(0, 12);
  }

  getFallbackBlocks() {
    // Fallback content when API is completely unavailable
    return [
      {
        id: 'fallback-1',
        class: 'Text',
        content: 'exploring digital aesthetics',
        generated_title: 'exploring digital aesthetics'
      },
      {
        id: 'fallback-2', 
        class: 'Text',
        content: 'visual research & curation',
        generated_title: 'visual research & curation'
      },
      {
        id: 'fallback-3',
        class: 'Text', 
        content: 'collections of inspiration',
        generated_title: 'collections of inspiration'
      },
      {
        id: 'fallback-4',
        class: 'Text',
        content: 'creative documentation',
        generated_title: 'creative documentation'  
      },
      {
        id: 'fallback-5',
        class: 'Text',
        content: 'mood & vibes archive',
        generated_title: 'mood & vibes archive'
      }
    ];
  }

  hideLoading() {
    this.loading.style.opacity = '0';
    setTimeout(() => {
      this.loading.style.display = 'none';
    }, 500);
  }

  showError() {
    console.log('Showing error message');
    this.loading.innerHTML = '<span class="blink">> using_fallback_vibes.exe</span>';
    this.loading.style.display = 'block';
    this.loading.style.opacity = '1';
    
    // Hide after a few seconds
    setTimeout(() => {
      this.loading.style.opacity = '0';
      setTimeout(() => {
        this.loading.style.display = 'none';
      }, 500);
    }, 2000);
  }

  showApiInfo() {
    // Add debug info for API testing
    const debugInfo = document.createElement('div');
    debugInfo.style.cssText = `
      position: fixed;
      bottom: 10px;
      right: 10px;
      font-family: 'Inconsolata', monospace;
      font-size: 9px;
      color: var(--secondary-text-color);
      opacity: 0.5;
      z-index: 1000;
    `;
    debugInfo.innerHTML = 'vibes sourced from are.na API';
    document.body.appendChild(debugInfo);
  }

  displayBlocks(blocks) {
    console.log(`Displaying ${blocks.length} blocks`);
    if (!blocks || blocks.length === 0) {
      console.log('No blocks to display');
      return;
    }
    
    blocks.forEach((block, index) => {
      setTimeout(() => {
        console.log(`Adding block ${index}:`, block);
        this.addBlock(block);
      }, index * this.animationDelay);
    });
  }

  addBlock(blockData) {
    const blockElement = this.createBlockElement(blockData);
    const { width, height } = this.getBlockDimensions(blockData);
    const { x, y } = this.generatePosition(width, height);

    blockElement.style.left = `${x}px`;
    blockElement.style.top = `${y}px`;
    blockElement.style.width = `${width}px`;
    blockElement.style.height = `${height}px`;

    // Random rotation
    const rotation = (Math.random() - 0.5) * 15;
    blockElement.style.transform = `rotate(${rotation}deg) scale(0.8)`;
    blockElement.style.opacity = '0';

    this.container.appendChild(blockElement);
    this.placedBlocks.push({ x, y, width, height });

    // Animate in
    setTimeout(() => {
      blockElement.style.opacity = '1';
      blockElement.style.transform = blockElement.style.transform.replace('scale(0.8)', 'scale(1)');
    }, 100);
  }

  createBlockElement(blockData) {
    const element = document.createElement('div');
    element.className = 'block-item';
    element.setAttribute('data-block-id', blockData.id);

    switch (blockData.class) {
      case 'Image':
        if (blockData.image && blockData.image.large) {
          element.innerHTML = `
            <img src="${blockData.image.large.url}" 
                 alt="${blockData.title || ''}" 
                 class="block-image" 
                 loading="lazy" />
          `;
        }
        break;

      case 'Text':
        element.innerHTML = `
          <div class="block-text">
            <div class="block-content">${this.truncateText(blockData.content || blockData.generated_title || 'untitled', 100)}</div>
          </div>
        `;
        break;

      case 'Link':
        element.innerHTML = `
          <div class="block-link">
            ${blockData.image && blockData.image.large ? 
              `<img src="${blockData.image.large.url}" class="block-image" loading="lazy" />` : 
              `<div class="block-text">
                <div class="block-title">${this.truncateText(blockData.title || blockData.generated_title || 'link', 60)}</div>
                ${blockData.source ? `<div class="block-source">${new URL(blockData.source.url).hostname}</div>` : ''}
              </div>`
            }
          </div>
        `;
        break;

      default:
        element.innerHTML = `
          <div class="block-text">
            <div class="block-content">${blockData.class}</div>
          </div>
        `;
    }

    // Add click handler
    element.addEventListener('click', () => this.handleBlockClick(blockData));

    return element;
  }

  generatePosition(blockWidth, blockHeight, attempts = 50) {
    const containerRect = this.container.getBoundingClientRect();
    const padding = 60; // Increased padding for less crowding

    for (let i = 0; i < attempts; i++) {
      const x = Math.random() * (containerRect.width - blockWidth - padding * 2) + padding;
      const y = Math.random() * (containerRect.height - blockHeight - padding * 2) + padding;

      const newRect = { x, y, width: blockWidth, height: blockHeight };

      if (!this.hasCollision(newRect)) {
        return { x, y };
      }
    }

    // Fallback position with more spacing
    return {
      x: Math.random() * (containerRect.width - blockWidth - padding * 2) + padding,
      y: Math.random() * (containerRect.height - blockHeight - padding * 2) + padding
    };
  }

  hasCollision(newRect) {
    const buffer = 50; // Increased buffer for more spacing
    return this.placedBlocks.some(block => {
      return !(newRect.x + newRect.width + buffer < block.x ||
               block.x + block.width + buffer < newRect.x ||
               newRect.y + newRect.height + buffer < block.y ||
               block.y + block.height + buffer < newRect.y);
    });
  }

  getBlockDimensions(blockData) {
    const minSize = 150;
    const maxSize = 400;

    switch (blockData.class) {
      case 'Image':
        if (blockData.image && blockData.image.original) {
          const aspectRatio = blockData.image.original.width / blockData.image.original.height;
          const width = Math.min(maxSize, Math.max(minSize, 240 + Math.random() * 120));
          return { width, height: width / aspectRatio };
        }
        return { width: 280, height: 280 };

      case 'Text':
        const textLength = (blockData.content || blockData.generated_title || '').length;
        const size = Math.min(maxSize, Math.max(minSize, 180 + textLength * 0.5));
        return { width: size, height: size * 0.75 };

      case 'Link':
        return { width: 300, height: 200 };

      default:
        return { width: 220, height: 220 };
    }
  }

  truncateText(text, maxLength) {
    if (!text) return '';
    return text.length > maxLength ? text.substring(0, maxLength) + '...' : text;
  }

  handleBlockClick(blockData) {
    if (blockData.source && blockData.source.url) {
      window.open(blockData.source.url, '_blank');
    }
  }

  shuffleArray(array) {
    for (let i = array.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [array[i], array[j]] = [array[j], array[i]];
    }
  }
}

// Spotify Integration
class SpotifyVibes {
  constructor() {
    this.container = document.getElementById('spotify-tracks');
    this.clientId = 'YOUR_SPOTIFY_CLIENT_ID'; // Replace with your client ID
    this.redirectUri = window.location.origin + '/vibes/';
    this.scope = 'user-read-recently-played';
  }

  async init() {
    // Check if we have an access token
    const token = this.getAccessToken();
    
    if (token) {
      await this.fetchRecentTracks(token);
    } else {
      this.showAuthButton();
    }
  }

  getAccessToken() {
    // Check URL hash for token
    const hash = window.location.hash.substring(1);
    const params = new URLSearchParams(hash);
    const token = params.get('access_token');
    
    if (token) {
      // Store token in sessionStorage
      sessionStorage.setItem('spotify_token', token);
      // Clean up URL
      window.history.replaceState(null, null, window.location.pathname);
      return token;
    }
    
    // Check sessionStorage for existing token
    return sessionStorage.getItem('spotify_token');
  }

  showAuthButton() {
    this.container.innerHTML = `
      <button class="spotify-auth-btn" onclick="spotifyVibes.authenticate()">
        > connect_spotify.exe
      </button>
    `;
  }

  authenticate() {
    const authUrl = `https://accounts.spotify.com/authorize?` +
      `client_id=${this.clientId}&` +
      `response_type=token&` +
      `redirect_uri=${encodeURIComponent(this.redirectUri)}&` +
      `scope=${this.scope}`;
    
    window.location.href = authUrl;
  }

  async fetchRecentTracks(token) {
    try {
      const response = await fetch('https://api.spotify.com/v1/me/player/recently-played?limit=10', {
        headers: {
          'Authorization': `Bearer ${token}`
        }
      });

      if (!response.ok) {
        if (response.status === 401) {
          // Token expired
          sessionStorage.removeItem('spotify_token');
          this.showAuthButton();
          return;
        }
        throw new Error('Failed to fetch tracks');
      }

      const data = await response.json();
      this.displayTracks(data.items);
    } catch (error) {
      console.error('Error fetching Spotify data:', error);
      this.showFallbackTracks();
    }
  }

  displayTracks(tracks) {
    if (!tracks || tracks.length === 0) {
      this.showFallbackTracks();
      return;
    }

    const tracksHtml = tracks.map((item, index) => {
      const track = item.track;
      const artists = track.artists.map(a => a.name).join(', ');
      const playedAt = new Date(item.played_at);
      const timeAgo = this.getTimeAgo(playedAt);
      
      return `
        <div class="spotify-track" style="animation-delay: ${index * 100}ms">
          <div class="track-info">
            ${track.album.images.length > 0 ? 
              `<img src="${track.album.images[2].url}" alt="${track.album.name}" class="track-album-art" />` : 
              '<div class="track-album-art-placeholder"></div>'
            }
            <div class="track-details">
              <a href="${track.external_urls.spotify}" target="_blank" class="track-name">${track.name}</a>
              <div class="track-artist">${artists}</div>
              <div class="track-time">${timeAgo}</div>
            </div>
          </div>
        </div>
      `;
    }).join('');

    this.container.innerHTML = tracksHtml;
  }

  showFallbackTracks() {
    // Show sample/placeholder tracks when API is unavailable
    const fallbackTracks = [
      { name: "dream sequence", artist: "unknown artist", time: "2 mins ago" },
      { name: "digital rain", artist: "system", time: "5 mins ago" },
      { name: "void walker", artist: "null", time: "12 mins ago" },
      { name: "binary sunset", artist: "0x1", time: "23 mins ago" },
      { name: "neural patterns", artist: "ai", time: "45 mins ago" }
    ];

    const tracksHtml = fallbackTracks.map((track, index) => `
      <div class="spotify-track" style="animation-delay: ${index * 100}ms">
        <div class="track-info">
          <div class="track-album-art-placeholder"></div>
          <div class="track-details">
            <div class="track-name">${track.name}</div>
            <div class="track-artist">${track.artist}</div>
            <div class="track-time">${track.time}</div>
          </div>
        </div>
      </div>
    `).join('');

    this.container.innerHTML = tracksHtml;
  }

  getTimeAgo(date) {
    const seconds = Math.floor((new Date() - date) / 1000);
    
    if (seconds < 60) return 'just now';
    const minutes = Math.floor(seconds / 60);
    if (minutes < 60) return `${minutes} min${minutes > 1 ? 's' : ''} ago`;
    const hours = Math.floor(minutes / 60);
    if (hours < 24) return `${hours} hour${hours > 1 ? 's' : ''} ago`;
    const days = Math.floor(hours / 24);
    return `${days} day${days > 1 ? 's' : ''} ago`;
  }
}

let spotifyVibes;

// Initialize when page loads
document.addEventListener('DOMContentLoaded', () => {
  const vibes = new ArenaVibes();
  vibes.init();
  
  spotifyVibes = new SpotifyVibes();
  spotifyVibes.init();
});
</script>

<style>
.vibes-container {
  position: relative;
  width: 100%;
  min-height: 100vh;
  overflow: hidden;
  background-color: var(--background-color);
  padding: 0;
  margin: 0;
}

.loading {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  font-family: 'Inconsolata', monospace;
  font-size: 13px;
  color: var(--text-color);
  z-index: 1000;
  transition: opacity 0.5s ease;
}

.block-item {
  position: absolute;
  border-radius: 4px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  transition: all 0.3s ease;
  cursor: pointer;
  user-select: none;
  z-index: 1;
}

.block-item:hover {
  transform: scale(1.05) !important;
  z-index: 100 !important;
  box-shadow: 0 4px 16px rgba(0,0,0,0.2);
}

.block-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 4px;
  display: block;
}

.block-text {
  padding: 20px;
  background-color: var(--background-color);
  border: 1px solid var(--border);
  border-radius: 4px;
  height: 100%;
  box-sizing: border-box;
  overflow: hidden;
}

.block-content {
  font-family: 'Inconsolata', monospace;
  font-size: 14px;
  line-height: 1.5;
  color: var(--text-color);
  word-wrap: break-word;
}

.block-link {
  background-color: var(--background-color);
  border: 1px solid var(--border);
  border-radius: 4px;
  overflow: hidden;
  height: 100%;
}

.block-title {
  font-family: 'Inconsolata', monospace;
  font-size: 14px;
  font-weight: bold;
  color: var(--text-color);
  margin-bottom: 6px;
  line-height: 1.4;
}

.block-source {
  font-family: 'Inconsolata', monospace;
  font-size: 11px;
  color: var(--secondary-text-color);
  opacity: 0.7;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .vibes-container {
    min-height: calc(100vh - 140px);
  }
  
  .block-item {
    max-width: 120px !important;
    max-height: 120px !important;
  }
  
  .block-content,
  .block-title {
    font-size: 10px;
  }
  
  .block-source {
    font-size: 8px;
  }
}

/* Dark theme specific adjustments */
[data-theme="dark"] .block-text,
[data-theme="dark"] .block-link {
  background-color: rgba(45, 45, 45, 0.8);
  border-color: rgba(225, 225, 225, 0.1);
}

[data-theme="dark"] .block-item:hover {
  box-shadow: 0 4px 16px rgba(255,255,255,0.1);
}

/* Light theme specific adjustments */
[data-theme="light"] .block-text,
[data-theme="light"] .block-link {
  background-color: rgba(255, 255, 255, 0.9);
  border-color: rgba(0, 0, 0, 0.1);
}

[data-theme="light"] .block-item:hover {
  box-shadow: 0 4px 16px rgba(0,0,0,0.15);
}

/* Spotify Styles */
.spotify-container {
  margin-top: 80px;
  padding: 40px 20px;
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
}

.spotify-title {
  font-family: 'Inconsolata', monospace;
  font-size: 16px;
  color: var(--text-color);
  margin-bottom: 30px;
  font-weight: normal;
}

.spotify-tracks {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.spotify-loading {
  font-family: 'Inconsolata', monospace;
  font-size: 13px;
  color: var(--text-color);
  opacity: 0.7;
}

.spotify-auth-btn {
  font-family: 'Inconsolata', monospace;
  font-size: 14px;
  background: none;
  border: 1px dashed var(--text-color);
  color: var(--text-color);
  padding: 10px 20px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.spotify-auth-btn:hover {
  background-color: var(--text-color);
  color: var(--background-color);
}

.spotify-track {
  opacity: 0;
  animation: fadeInUp 0.5s ease forwards;
  border-bottom: 1px dashed rgba(0,0,0,0.1);
  padding-bottom: 15px;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.track-info {
  display: flex;
  align-items: center;
  gap: 15px;
}

.track-album-art {
  width: 50px;
  height: 50px;
  object-fit: cover;
  border-radius: 3px;
}

.track-album-art-placeholder {
  width: 50px;
  height: 50px;
  background: linear-gradient(45deg, var(--border) 25%, transparent 25%, transparent 75%, var(--border) 75%, var(--border)),
              linear-gradient(45deg, var(--border) 25%, transparent 25%, transparent 75%, var(--border) 75%, var(--border));
  background-size: 10px 10px;
  background-position: 0 0, 5px 5px;
  border-radius: 3px;
  opacity: 0.3;
}

.track-details {
  flex: 1;
}

.track-name {
  font-family: 'Inconsolata', monospace;
  font-size: 14px;
  font-weight: bold;
  color: var(--text-color);
  text-decoration: none;
  display: block;
  margin-bottom: 3px;
}

.track-name:hover {
  text-decoration: underline;
}

.track-artist {
  font-family: 'Inconsolata', monospace;
  font-size: 13px;
  color: var(--text-color);
  opacity: 0.8;
  margin-bottom: 2px;
}

.track-time {
  font-family: 'Inconsolata', monospace;
  font-size: 11px;
  color: var(--text-color);
  opacity: 0.5;
}

/* Dark theme Spotify adjustments */
[data-theme="dark"] .spotify-track {
  border-bottom-color: rgba(255,255,255,0.1);
}

[data-theme="dark"] .track-album-art-placeholder {
  opacity: 0.2;
}

/* Mobile responsive for Spotify */
@media (max-width: 768px) {
  .spotify-container {
    padding: 20px 10px;
  }
  
  .track-album-art,
  .track-album-art-placeholder {
    width: 40px;
    height: 40px;
  }
  
  .track-name {
    font-size: 13px;
  }
  
  .track-artist {
    font-size: 12px;
  }
  
  .track-time {
    font-size: 10px;
  }
}
</style>