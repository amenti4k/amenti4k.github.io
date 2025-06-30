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
    const padding = 40; // Increased padding for less crowding

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
    const buffer = 30; // Increased buffer for more spacing
    return this.placedBlocks.some(block => {
      return !(newRect.x + newRect.width + buffer < block.x ||
               block.x + block.width + buffer < newRect.x ||
               newRect.y + newRect.height + buffer < block.y ||
               block.y + block.height + buffer < newRect.y);
    });
  }

  getBlockDimensions(blockData) {
    const minSize = 100;
    const maxSize = 280;

    switch (blockData.class) {
      case 'Image':
        if (blockData.image && blockData.image.original) {
          const aspectRatio = blockData.image.original.width / blockData.image.original.height;
          const width = Math.min(maxSize, Math.max(minSize, 160 + Math.random() * 80));
          return { width, height: width / aspectRatio };
        }
        return { width: 180, height: 180 };

      case 'Text':
        const textLength = (blockData.content || blockData.generated_title || '').length;
        const size = Math.min(maxSize, Math.max(minSize, 120 + textLength * 0.4));
        return { width: size, height: size * 0.75 };

      case 'Link':
        return { width: 200, height: 140 };

      default:
        return { width: 140, height: 140 };
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

// Initialize when page loads
document.addEventListener('DOMContentLoaded', () => {
  const vibes = new ArenaVibes();
  vibes.init();
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
  padding: 12px;
  background-color: var(--background-color);
  border: 1px solid var(--border);
  border-radius: 4px;
  height: 100%;
  box-sizing: border-box;
  overflow: hidden;
}

.block-content {
  font-family: 'Inconsolata', monospace;
  font-size: 11px;
  line-height: 1.4;
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
  font-size: 11px;
  font-weight: bold;
  color: var(--text-color);
  margin-bottom: 4px;
  line-height: 1.3;
}

.block-source {
  font-family: 'Inconsolata', monospace;
  font-size: 9px;
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
</style>