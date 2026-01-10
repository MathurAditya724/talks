<script setup lang="ts">
import { useNav } from "@slidev/client";
import seedrandom from "seedrandom";
import { computed, ref, watch } from "vue";

/**
 * Sentry-branded animated background
 * - Animated purple/blue/pink gradient
 * - Grainy texture overlay
 * - Floating geometric icons that reposition on slide change
 *
 * Frontmatter options:
 * - bgIntensity: number (0-1, default: 1)
 * - iconDensity: 'normal' | 'dense' (default: 'normal')
 * - glowSeed: string (default: 'sentry')
 */

const { currentSlideRoute } = useNav();

type IconType = "triangle" | "circle" | "x" | "zigzag" | "square" | "plus";

interface FloatingIcon {
	id: number;
	type: IconType;
	x: number;
	y: number;
	rotation: number;
	scale: number;
	opacity: number;
}

const formatter = computed(
	() => (currentSlideRoute.value.meta?.slide as any)?.frontmatter || {},
);
const bgIntensity = computed(() => +(formatter.value.bgIntensity ?? 1));
const iconDensity = computed(() => formatter.value.iconDensity || "normal");
const seed = computed(() => formatter.value.glowSeed || "sentry");

const densityMap = {
	normal: 20,
	dense: 30,
};

const iconTypes: IconType[] = [
	"triangle",
	"triangle",
	"circle",
	"circle",
	"x",
	"x",
	"x",
	"zigzag",
	"zigzag",
	"square",
	"plus",
];

function generateIcons(count: number, slideNo: number): FloatingIcon[] {
	const rng = seedrandom(`${seed.value}-icons-${slideNo}`);

	// Fixed 8x6 grid for maximum spacing (48 cells for ~20 icons)
	const cols = 8;
	const rows = 6;
	const cellWidth = 100 / cols;
	const cellHeight = 100 / rows;

	// Generate ALL grid positions first, then shuffle and pick
	const allPositions: Array<{ x: number; y: number }> = [];
	for (let row = 0; row < rows; row++) {
		for (let col = 0; col < cols; col++) {
			// Random position within this grid cell (with padding to avoid edges)
			const padding = 0.15;
			const x =
				col * cellWidth + cellWidth * (padding + rng() * (1 - 2 * padding));
			const y =
				row * cellHeight + cellHeight * (padding + rng() * (1 - 2 * padding));
			allPositions.push({ x, y });
		}
	}

	// Shuffle ALL positions first
	for (let i = allPositions.length - 1; i > 0; i--) {
		const j = Math.floor(rng() * (i + 1));
		[allPositions[i], allPositions[j]] = [allPositions[j], allPositions[i]];
	}

	// Take only the positions we need (now distributed across full grid)
	const positions = allPositions.slice(0, count);

	return Array.from({ length: count }, (_, i) => ({
		id: i,
		type: iconTypes[Math.floor(rng() * iconTypes.length)],
		x: positions[i]?.x ?? rng() * 100,
		y: positions[i]?.y ?? rng() * 100,
		rotation: rng() * 360,
		scale: 0.6 + rng() * 0.8,
		opacity: 0.1 + rng() * 0.2,
	}));
}

const iconCount = computed(() => densityMap[iconDensity.value] || 20);
const icons = ref<FloatingIcon[]>(
	generateIcons(iconCount.value, currentSlideRoute.value.no),
);

// Smoothly transition icons to new positions on slide change
watch(currentSlideRoute, () => {
	const newIcons = generateIcons(iconCount.value, currentSlideRoute.value.no);

	// Track which new positions are already taken
	const takenPositions = new Set<number>();

	// Find the closest available position for each icon (no duplicates)
	icons.value = icons.value.map((oldIcon) => {
		let bestIndex = -1;
		let bestDistance = Number.POSITIVE_INFINITY;

		// Find closest untaken position
		for (let i = 0; i < newIcons.length; i++) {
			if (takenPositions.has(i)) continue;

			const dx = newIcons[i].x - oldIcon.x;
			const dy = newIcons[i].y - oldIcon.y;
			const distance = dx * dx + dy * dy;

			if (distance < bestDistance) {
				bestDistance = distance;
				bestIndex = i;
			}
		}

		// Mark this position as taken
		if (bestIndex >= 0) {
			takenPositions.add(bestIndex);
		}

		const newIcon = newIcons[bestIndex] || newIcons[0];
		return {
			...oldIcon,
			x: newIcon.x,
			y: newIcon.y,
			rotation: newIcon.rotation,
			scale: newIcon.scale,
			opacity: newIcon.opacity,
		};
	});
});

// Gradient animation offset based on slide
const gradientOffset = computed(() => {
	return (currentSlideRoute.value.no * 30) % 360;
});
</script>

<template>
  <div class="sentry-bg" aria-hidden="true">
    <!-- Sentry Logo - Bottom Right -->
    <img 
      src="/sentry-logo.svg" 
      alt="Sentry" 
      class="sentry-logo"
    />
    
    <!-- Animated Gradient Layer -->
    <div 
      class="gradient-layer"
      :style="{ 
        opacity: bgIntensity,
        '--gradient-rotation': `${gradientOffset}deg`
      }"
    />
    
    <!-- Grain/Noise Texture Overlay -->
    <div class="grain-layer" />
    
    <!-- Floating Icons Layer -->
    <div class="icons-layer">
      <div
        v-for="icon in icons"
        :key="icon.id"
        class="floating-icon"
        :style="{
          left: `${icon.x}%`,
          top: `${icon.y}%`,
          transform: `rotate(${icon.rotation}deg) scale(${icon.scale})`,
          opacity: icon.opacity
        }"
      >
        <!-- Triangle (Warning style) -->
        <svg v-if="icon.type === 'triangle'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
          <path d="M12 2L2 22h20L12 2z" />
        </svg>
        
        <!-- Circle -->
        <svg v-else-if="icon.type === 'circle'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
          <circle cx="12" cy="12" r="10" />
        </svg>
        
        <!-- X Mark -->
        <svg v-else-if="icon.type === 'x'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
          <path d="M18 6L6 18M6 6l12 12" />
        </svg>
        
        <!-- Zigzag -->
        <svg v-else-if="icon.type === 'zigzag'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
          <polyline points="2,6 6,12 10,6 14,12 18,6 22,12" />
        </svg>
        
        <!-- Square -->
        <svg v-else-if="icon.type === 'square'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
          <rect x="3" y="3" width="18" height="18" rx="2" />
        </svg>
        
        <!-- Plus -->
        <svg v-else-if="icon.type === 'plus'" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
          <path d="M12 5v14M5 12h14" />
        </svg>
      </div>
    </div>
  </div>
</template>

<style scoped>
.sentry-bg {
  position: absolute;
  inset: 0;
  z-index: -10;
  overflow: hidden;
  pointer-events: none;
}

.sentry-logo {
  position: absolute;
  bottom: 1.5rem;
  right: 1.5rem;
  width: 32px;
  height: auto;
  opacity: 0.6;
  z-index: 10;
}

/* Animated Gradient */
.gradient-layer {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    calc(135deg + var(--gradient-rotation, 0deg)),
    #362D59 0%,
    #6C5FC7 25%,
    #4B3F9E 50%,
    #FA4E89 75%,
    #362D59 100%
  );
  background-size: 400% 400%;
  animation: gradientShift 20s ease infinite;
  transition: opacity 0.5s ease;
}

@keyframes gradientShift {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

/* Grain/Noise Texture - subtle */
.grain-layer {
  position: absolute;
  inset: 0;
  opacity: 0.15;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.7' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
  pointer-events: none;
  mix-blend-mode: soft-light;
}

/* Floating Icons */
.icons-layer {
  position: absolute;
  inset: 0;
}

.floating-icon {
  position: absolute;
  width: 32px;
  height: 32px;
  color: #B8AFF2;
  transition: all 2.5s cubic-bezier(0.4, 0, 0.2, 1);
  filter: blur(0.5px);
}

.floating-icon svg {
  width: 100%;
  height: 100%;
}

/* Subtle parallax-like depth effect */
.floating-icon:nth-child(3n) {
  filter: blur(1px);
}

.floating-icon:nth-child(5n) {
  filter: blur(0px);
}

.floating-icon:nth-child(7n) {
  filter: blur(1.5px);
}
</style>
