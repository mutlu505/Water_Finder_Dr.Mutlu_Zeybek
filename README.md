# Water_Finder_Dr.Mutlu_Zeybek
Water_Finder_Dr.Mutlu_Zeybek

import matplotlib.pyplot as plt
import matplotlib.patches as patches
from matplotlib.patches import Polygon, Circle
import numpy as np

# Set up the figure with high quality for publication
plt.rcParams["font.family"] = "serif"
plt.rcParams["font.size"] = 12
plt.rcParams["figure.dpi"] = 300
plt.rcParams["savefig.dpi"] = 300
plt.rcParams["axes.labelsize"] = 12
plt.rcParams["axes.titlesize"] = 14
plt.rcParams["legend.fontsize"] = 10
plt.rcParams["xtick.labelsize"] = 10
plt.rcParams["ytick.labelsize"] = 10

fig, ax = plt.subplots(1, 1, figsize=(13, 9))
fig.patch.set_facecolor("white")

# ============================================================================
# 1. SERPENTINITE BODY (background polygon)
# ============================================================================
serpentinite_x = [0, 2, 4, 5.5, 7, 8, 9, 10, 11, 12, 10, 8, 5, 2, 0]
serpentinite_y = [0, 0.5, 0.2, 1, 0.8, 1.2, 1, 0.5, 0, 2, 3.5, 4, 4.5, 3.8, 2.5]
serpentinite = Polygon(
    list(zip(serpentinite_x, serpentinite_y)),
    facecolor="#D2A679",
    edgecolor="#8B5A2B",
    linewidth=2,
    alpha=0.7,
    label="Serpentinite Body",
)
ax.add_patch(serpentinite)

# Add texture to serpentinite
np.random.seed(42)
for _ in range(150):
    x = np.random.uniform(0, 12)
    y = np.random.uniform(0, 4.5)
    if serpentinite.get_path().contains_point((x, y)):
        ax.plot(x, y, "o", color="#8B5A2B", markersize=1.5, alpha=0.3)

# ============================================================================
# 2. FAULT TRACE (coincident with spring location)
# ============================================================================
fault_x = [4.5, 5.5, 6.4, 7.2, 8.0, 8.8, 9.5]
fault_y = [1.0, 1.5, 2.0, 2.4, 2.8, 3.2, 3.6]
ax.plot(
    fault_x,
    fault_y,
    color="red",
    linewidth=3,
    linestyle="-",
    marker="o",
    markersize=5,
    markerfacecolor="red",
    markeredgecolor="darkred",
    label="Fault Trace",
    zorder=5,
)

# Add fault ticks
for i in range(len(fault_x) - 1):
    angle = np.arctan2(fault_y[i + 1] - fault_y[i], fault_x[i + 1] - fault_x[i])
    perp = angle + np.pi / 2
    mid_x = (fault_x[i] + fault_x[i + 1]) / 2
    mid_y = (fault_y[i] + fault_y[i + 1]) / 2
    offset = 0.12
    ax.plot(
        [mid_x - offset * np.cos(perp), mid_x + offset * np.cos(perp)],
        [mid_y - offset * np.sin(perp), mid_y + offset * np.sin(perp)],
        color="darkred",
        linewidth=1.5,
    )

# ============================================================================
# 3. INDICATOR VEGETATION ZONES (colored patches)
# ============================================================================

# Phragmites australis (Reed) zones - closest to spring
phragmites1 = Circle(
    (7.2, 2.4),
    0.55,
    facecolor="#90EE90",
    edgecolor="#2E8B57",
    linewidth=1.5,
    alpha=0.55,
    zorder=1,
)
ax.add_patch(phragmites1)

phragmites2 = Circle(
    (8.1, 2.9),
    0.5,
    facecolor="#90EE90",
    edgecolor="#2E8B57",
    linewidth=1.5,
    alpha=0.55,
    zorder=1,
)
ax.add_patch(phragmites2)

# Liquidambar orientalis (Sweetgum) zones - intermediate distance
liquidambar1 = Circle(
    (6.3, 1.9),
    0.7,
    facecolor="#228B22",
    edgecolor="#006400",
    linewidth=1.5,
    alpha=0.5,
    zorder=1,
)
ax.add_patch(liquidambar1)

liquidambar2 = Circle(
    (8.9, 3.3),
    0.65,
    facecolor="#228B22",
    edgecolor="#006400",
    linewidth=1.5,
    alpha=0.5,
    zorder=1,
)
ax.add_patch(liquidambar2)

# Erica manipuliflora (Heath) zones - upslope recharge area
erica1 = Circle(
    (5.3, 1.4),
    0.8,
    facecolor="#8B7355",
    edgecolor="#5C4033",
    linewidth=1.5,
    alpha=0.5,
    zorder=1,
)
ax.add_patch(erica1)

erica2 = Circle(
    (9.7, 3.7),
    0.7,
    facecolor="#8B7355",
    edgecolor="#5C4033",
    linewidth=1.5,
    alpha=0.5,
    zorder=1,
)
ax.add_patch(erica2)

# Pinus brutia (Turkish Pine) high-vigor zones - fracture trace indicators
pinus1 = Circle(
    (4.2, 1.0),
    0.85,
    facecolor="#4A7A4A",
    edgecolor="#2C4A2C",
    linewidth=1.5,
    alpha=0.4,
    zorder=1,
)
ax.add_patch(pinus1)

pinus2 = Circle(
    (10.3, 4.0),
    0.75,
    facecolor="#4A7A4A",
    edgecolor="#2C4A2C",
    linewidth=1.5,
    alpha=0.4,
    zorder=1,
)
ax.add_patch(pinus2)

# ============================================================================
# 4. PREDICTED SPRING LOCATION (coincident with fault)
# ============================================================================
spring_x, spring_y = 7.2, 2.4
ax.plot(
    spring_x,
    spring_y,
    "o",
    color="#1E90FF",
    markersize=16,
    markerfacecolor="#1E90FF",
    markeredgecolor="darkblue",
    markeredgewidth=2.5,
    zorder=10,
    label="Predicted Spring Location",
)

# Add water ripple effect
for r in [0.25, 0.45, 0.65]:
    ripple = Circle(
        (spring_x, spring_y),
        r,
        facecolor="none",
        edgecolor="#1E90FF",
        linewidth=1.5,
        alpha=0.6,
        zorder=9,
    )
    ax.add_patch(ripple)

# ============================================================================
# 5. VEGETATION SYMBOLS (placed INSIDE their respective circles)
# ============================================================================


def draw_reed(x, y):
    """Draw Phragmites australis symbol"""
    ax.plot([x, x], [y - 0.1, y + 0.2], color="#2E8B57", linewidth=2.5)
    for offset in [-0.04, 0, 0.04]:
        ax.plot(
            [x - 0.08, x + 0.08],
            [y + 0.08, y + 0.08],
            color="#2E8B57",
            linewidth=1.5,
            alpha=0.8,
        )
    ax.fill(
        [x - 0.04, x, x + 0.04],
        [y + 0.2, y + 0.32, y + 0.2],
        color="#D2B48C",
        edgecolor="#8B7355",
        alpha=0.8,
    )


def draw_sweetgum(x, y):
    """Draw Liquidambar orientalis tree"""
    ax.plot([x, x], [y - 0.1, y + 0.35], color="#8B5A2B", linewidth=3)
    t = np.linspace(0, 2 * np.pi, 20)
    r = 0.22
    canopy_x = x + r * np.cos(t)
    canopy_y = y + 0.3 + r * np.sin(t) * 0.8
    ax.fill(canopy_x, canopy_y, color="#228B22", edgecolor="#006400", alpha=0.95)
    ax.fill(
        [x - 0.15, x, x + 0.15],
        [y + 0.42, y + 0.58, y + 0.42],
        color="#2E8B57",
        edgecolor="#006400",
    )


def draw_heath(x, y):
    """Draw Erica manipuliflora shrub"""
    for offset_x in [-0.1, 0, 0.1]:
        ax.plot(
            [x + offset_x, x + offset_x],
            [y - 0.05, y + 0.15],
            color="#5C4033",
            linewidth=2,
        )
        ax.fill(
            [x + offset_x - 0.08, x + offset_x, x + offset_x + 0.08],
            [y + 0.05, y + 0.22, y + 0.05],
            color="#8B7355",
            edgecolor="#5C4033",
            alpha=0.95,
        )


def draw_pine(x, y):
    """Draw Pinus brutia tree"""
    ax.plot([x, x], [y - 0.1, y + 0.3], color="#5C4033", linewidth=3)
    tiers = [(0.4, 0.16), (0.28, 0.12), (0.18, 0.1)]
    for tier_y, tier_r in tiers:
        ax.fill(
            [x - tier_r, x, x + tier_r],
            [y + tier_y - 0.1, y + tier_y + 0.08, y + tier_y - 0.1],
            color="#4A7A4A",
            edgecolor="#2C4A2C",
            alpha=0.95,
        )


# Place vegetation symbols INSIDE circular zones
draw_reed(7.2, 2.3)
draw_reed(7.0, 2.5)
draw_reed(7.4, 2.2)
draw_reed(8.1, 2.8)
draw_reed(8.0, 3.0)

draw_sweetgum(6.3, 1.8)
draw_sweetgum(6.1, 2.0)
draw_sweetgum(8.9, 3.2)
draw_sweetgum(8.7, 3.4)

draw_heath(5.3, 1.3)
draw_heath(5.1, 1.5)
draw_heath(5.5, 1.2)
draw_heath(9.7, 3.6)
draw_heath(9.5, 3.8)

draw_pine(4.2, 0.9)
draw_pine(4.0, 1.1)
draw_pine(4.4, 1.0)
draw_pine(10.3, 3.9)
draw_pine(10.1, 4.1)
draw_pine(10.5, 3.8)

# ============================================================================
# 6. TEXT LABELS POSITIONED TO THE RIGHT OF EACH CIRCLE
# ============================================================================

# Phragmites labels (to the right of each light green circle)
ax.text(
    7.86,
    2.40,
    "Phragmites australis",
    fontsize=11,
    fontweight="bold",
    va="center",
    bbox=dict(
        boxstyle="round", facecolor="white", alpha=0.9, edgecolor="#2E8B57", linewidth=2
    ),
)
ax.text(
    8.7,
    3.00,
    "Phragmites australis",
    fontsize=11,
    fontweight="bold",
    va="center",
    bbox=dict(
        boxstyle="round", facecolor="white", alpha=0.9, edgecolor="#2E8B57", linewidth=2
    ),
)

# Liquidambar labels (to the right of each dark green circle)
ax.text(
    7.1,
    1.9,
    "Liquidambar orientalis",
    fontsize=11,
    fontweight="bold",
    va="center",
    bbox=dict(
        boxstyle="round", facecolor="white", alpha=0.9, edgecolor="#006400", linewidth=2
    ),
)
ax.text(
    9.65,
    3.3,
    "Liquidambar orientalis",
    fontsize=11,
    fontweight="bold",
    va="center",
    bbox=dict(
        boxstyle="round", facecolor="white", alpha=0.9, edgecolor="#006400", linewidth=2
    ),
)

# Erica labels (to the right of each brown circle)
ax.text(
    6.2,
    1.4,
    "Erica manipuliflora",
    fontsize=11,
    fontweight="bold",
    va="center",
    bbox=dict(
        boxstyle="round", facecolor="white", alpha=0.9, edgecolor="#5C4033", linewidth=2
    ),
)
ax.text(
    10.5,
    3.7,
    "Erica manipuliflora",
    fontsize=11,
    fontweight="bold",
    va="center",
    bbox=dict(
        boxstyle="round", facecolor="white", alpha=0.9, edgecolor="#5C4033", linewidth=2
    ),
)

# Pinus labels (to the right of each forest green circle)
ax.text(
    5.15,
    1.0,
    "Pinus brutia\n(high vigor)",
    fontsize=10,
    fontweight="bold",
    va="center",
    bbox=dict(
        boxstyle="round", facecolor="white", alpha=0.9, edgecolor="#2C4A2C", linewidth=2
    ),
)
ax.text(
    11.15,
    4.0,
    "Pinus brutia\n(high vigor)",
    fontsize=10,
    fontweight="bold",
    va="center",
    bbox=dict(
        boxstyle="round", facecolor="white", alpha=0.9, edgecolor="#2C4A2C", linewidth=2
    ),
)

# ============================================================================
# 7. SPRING LABEL (above the spring)
# ============================================================================
ax.annotate(
    "PREDICTED\nSPRING",
    xy=(spring_x, spring_y),
    xytext=(spring_x + 0.0, spring_y + 1.0),
    fontsize=12,
    fontweight="bold",
    color="darkblue",
    ha="center",
    arrowprops=dict(arrowstyle="->", color="darkblue", lw=2.5),
    bbox=dict(
        boxstyle="round",
        facecolor="lightblue",
        alpha=0.95,
        edgecolor="darkblue",
        linewidth=2,
    ),
)

# ============================================================================
# 8. GROUNDWATER FLOW ARROWS (from high elevation to low elevation)
# ============================================================================

# Arrow from upper-left recharge area
ax.annotate(
    "",
    xy=(spring_x - 0.5, spring_y + 0.2),
    xytext=(4.5, 2.8),
    arrowprops=dict(
        arrowstyle="->", color="darkblue", lw=3, alpha=0.8, shrinkA=0, shrinkB=0
    ),
)
ax.annotate(
    "",
    xy=(spring_x - 0.2, spring_y + 0.1),
    xytext=(5.2, 2.2),
    arrowprops=dict(
        arrowstyle="->", color="darkblue", lw=3, alpha=0.8, shrinkA=0, shrinkB=0
    ),
)

# Arrow from upper-right recharge area
ax.annotate(
    "",
    xy=(spring_x + 0.3, spring_y + 0.19),
    xytext=(8.5, 3.3),
    arrowprops=dict(
        arrowstyle="->", color="darkblue", lw=3, alpha=0.8, shrinkA=0, shrinkB=0
    ),
)
ax.annotate(
    "",
    xy=(spring_x + 0.5, spring_y + 0.1),
    xytext=(9.0, 2.9),
    arrowprops=dict(
        arrowstyle="->", color="darkblue", lw=3, alpha=0.8, shrinkA=0, shrinkB=0
    ),
)

# Long arrow from top along fault
ax.annotate(
    "",
    xy=(spring_x, spring_y - 0.1),
    xytext=(spring_x + 0.3, spring_y + 0.9),
    arrowprops=dict(
        arrowstyle="->", color="darkblue", lw=3, alpha=0.8, linestyle="dashed"
    ),
)

# Groundwater flow direction label
ax.text(
    4.2,
    2.6,
    "Groundwater Flow",
    fontsize=11,
    ha="center",
    rotation=25,
    alpha=0.9,
    fontweight="bold",
    bbox=dict(boxstyle="round", facecolor="white", alpha=0.85, edgecolor="darkblue"),
)
ax.text(
    8.3,
    0.5,
    "(Low → High Elevation)",
    fontsize=10,
    ha="center",
    alpha=0.8,
    bbox=dict(boxstyle="round", facecolor="white", alpha=0.7),
)

# Elevation labels
ax.text(
    5.0,
    4.7,
    "↑ HIGHER\nELEVATION",
    fontsize=10,
    ha="center",
    alpha=0.8,
    bbox=dict(boxstyle="round", facecolor="white", alpha=0.7),
    fontweight="bold",
)
ax.text(
    5.0,
    -0.3,
    "↓ LOWER\nELEVATION",
    fontsize=10,
    ha="center",
    alpha=0.8,
    bbox=dict(boxstyle="round", facecolor="white", alpha=0.7),
    fontweight="bold",
)

# ============================================================================
# 9. NORTH ARROW (top-right corner)
# ============================================================================
north_x, north_y = 12.7, 4.8
ax.annotate(
    "N",
    xy=(north_x, north_y),
    xytext=(north_x, north_y - 0.4),
    arrowprops=dict(arrowstyle="->", color="black", lw=3, relpos=(0.5, 1)),
    fontsize=16,
    fontweight="bold",
    ha="center",
    va="bottom",
)
compass = Circle(
    (north_x, north_y - 0.18),
    0.3,
    facecolor="none",
    edgecolor="black",
    linewidth=1.5,
    alpha=0.6,
)
ax.add_patch(compass)

# ============================================================================
# 10. AXES: X-COORDINATE (EAST) AND Y-COORDINATE (NORTH/DEPTH)
# ============================================================================

# Set axis limits
ax.set_xlim(-1.8, 13.5)
ax.set_ylim(-0.8, 5.2)

# X-axis (East coordinate)
ax.set_xlabel("X-Coordinate (East)", fontsize=13, fontweight="bold", labelpad=10)
ax.xaxis.set_label_position("bottom")
ax.spines["bottom"].set_visible(True)
ax.spines["bottom"].set_position(("outward", 10))
ax.set_xticks([0, 2, 4, 6, 8, 10, 12])
ax.set_xticklabels(["0", "2", "4", "6", "8", "10", "12 km (East)"], fontsize=10)

# Y-axis (North/Depth)
ax.set_ylabel(
    "Y-Coordinate (North / Depth)", fontsize=13, fontweight="bold", labelpad=10
)
ax.yaxis.set_label_position("left")
ax.spines["left"].set_visible(True)
ax.spines["left"].set_position(("outward", 10))
ax.set_yticks([0, 1, 2, 3, 4])
ax.set_yticklabels(["0", "1", "2", "3", "4 km (North)"], fontsize=10)

# Depth annotation
ax.text(
    12.3,
    0.5,
    "↑ Depth increases\n↓ downward",
    fontsize=8,
    ha="center",
    alpha=0.6,
    style="italic",
    bbox=dict(boxstyle="round", facecolor="white", alpha=0.5),
)

# Light grid
ax.grid(True, linestyle=":", alpha=0.25, color="gray")

# ============================================================================
# 11. COORDINATE SYSTEM LABELS (x₁, y₁, etc.)
# ============================================================================
coords_x = [0, 2, 4, 6, 8, 10, 12]
coords_y = [0, 1, 2, 3, 4]
for i, x in enumerate(coords_x[1:], 1):
    ax.text(
        x,
        -0.6,
        f"x_{i}",
        fontsize=9,
        ha="center",
        color="gray",
        alpha=0.8,
        fontweight="bold",
    )
for i, y in enumerate(coords_y[1:], 1):
    ax.text(
        -1.4,
        y,
        f"y_{i}",
        fontsize=9,
        va="center",
        color="gray",
        alpha=0.8,
        fontweight="bold",
    )

# ============================================================================
# 12. SCALE BAR
# ============================================================================
scale_start_x, scale_start_y = 10.50, -0.1
scale_length = 2.0
ax.plot(
    [scale_start_x, scale_start_x + scale_length],
    [scale_start_y, scale_start_y],
    "k-",
    linewidth=3,
)
ax.plot(
    [scale_start_x, scale_start_x],
    [scale_start_y - 0.1, scale_start_y + 0.1],
    "k-",
    linewidth=2.5,
)
ax.plot(
    [scale_start_x + scale_length, scale_start_x + scale_length],
    [scale_start_y - 0.1, scale_start_y + 0.1],
    "k-",
    linewidth=2.5,
)
ax.text(
    scale_start_x + scale_length / 2,
    scale_start_y - 0.25,
    "1 km",
    fontsize=11,
    ha="center",
    fontweight="bold",
)

# ============================================================================
# 13. LEGEND (top-left corner)
# ============================================================================

legend_elements = [
    patches.Patch(
        facecolor="#D2A679", alpha=0.7, edgecolor="#8B5A2B", label="Serpentinite Body"
    ),
    plt.Line2D([0], [0], color="red", linewidth=2.5, label="Fault Trace"),
    patches.Patch(facecolor="#90EE90", alpha=0.55, label="Phragmites australis (Reed)"),
    patches.Patch(
        facecolor="#228B22", alpha=0.5, label="Liquidambar orientalis (Sweetgum)"
    ),
    patches.Patch(facecolor="#8B7355", alpha=0.5, label="Erica manipuliflora (Heath)"),
    patches.Patch(facecolor="#4A7A4A", alpha=0.4, label="Pinus brutia (High vigor)"),
    plt.Line2D(
        [0],
        [0],
        marker="o",
        color="w",
        markerfacecolor="#1E90FF",
        markersize=12,
        markeredgecolor="darkblue",
        markeredgewidth=2.5,
        label="Predicted Spring",
    ),
]

ax.legend(
    handles=legend_elements,
    loc="upper left",
    frameon=True,
    fontsize=10,
    bbox_to_anchor=(0.05, 1.0),
    ncol=1,
    framealpha=0.95,
    edgecolor="black",
    fancybox=True,
    shadow=True,
)

# ============================================================================
# 14. TITLE
# ============================================================================

ax.set_title(
    "Figure 4: Simplified Conceptual Model for Natural Drinking Water Targeting\n"
    "Serpentinite Terrain, Marmaris Peridotite, SW Türkiye",
    fontsize=14,
    fontweight="bold",
    pad=25,
)

# ============================================================================
# 15. SAVE THE FIGURE
# ============================================================================
plt.tight_layout()
plt.savefig(
    "Figure_4_Conceptual_Model.png", dpi=300, bbox_inches="tight", facecolor="white"
)
plt.savefig("Figure_4_Conceptual_Model.pdf", bbox_inches="tight", facecolor="white")
plt.savefig("Figure_4_Conceptual_Model.svg", bbox_inches="tight", facecolor="white")
plt.show()

print("=" * 70)
print("Figure 4 has been saved successfully!")
print("=" * 70)
print("\nKEY MODIFICATION MADE:")
print("  ✓ All text labels positioned to the RIGHT of their respective circles")
print("\nLabel positions:")
print("  • Phragmites australis → right of light green circles (x=7.85, 8.7)")
print("  • Liquidambar orientalis → right of dark green circles (x=7.1, 9.65)")
print("  • Erica manipuliflora → right of brown circles (x=6.2, 10.5)")
print("  • Pinus brutia → right of forest green circles (x=5.15, 11.15)")
print("=" * 70)

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

import matplotlib.pyplot as plt
import matplotlib.patches as patches
from matplotlib.path import Path

fig, ax = plt.subplots(1, 1, figsize=(12, 10))
ax.set_xlim(0, 10)
ax.set_ylim(0, 12)
ax.axis("off")

# Box style
box_style = dict(
    boxstyle="round,pad=0.3", edgecolor="black", facecolor="lightblue", linewidth=2
)
decision_style = dict(
    boxstyle="round,pad=0.3", edgecolor="black", facecolor="lightyellow", linewidth=2
)
result_style = dict(
    boxstyle="round,pad=0.3", edgecolor="black", facecolor="lightgreen", linewidth=2
)
failure_style = dict(
    boxstyle="round,pad=0.3", edgecolor="black", facecolor="lightcoral", linewidth=2
)

# Step 1
ax.text(
    5,
    11,
    "Step 1: Delineate serpentinite body\n(geological map or remote sensing)",
    ha="center",
    va="center",
    fontsize=10,
    weight="bold",
    bbox=box_style,
)

# Arrow
ax.annotate(
    "", xy=(5, 10.2), xytext=(5, 10.6), arrowprops=dict(arrowstyle="->", lw=1.5)
)

# Step 2
ax.text(
    5,
    9.5,
    "Step 2: Map fault traces within serpentinite\n(aerial imagery or field reconnaissance)",
    ha="center",
    va="center",
    fontsize=10,
    weight="bold",
    bbox=box_style,
)

ax.annotate("", xy=(5, 8.7), xytext=(5, 9.1), arrowprops=dict(arrowstyle="->", lw=1.5))

# Step 3
ax.text(
    5,
    8.0,
    "Step 3: Identify indicator vegetation zones\n(Phragmites, Liquidambar, Erica, high-vigor Pinus)",
    ha="center",
    va="center",
    fontsize=10,
    weight="bold",
    bbox=box_style,
)

ax.annotate("", xy=(5, 7.2), xytext=(5, 7.6), arrowprops=dict(arrowstyle="->", lw=1.5))

# Decision diamond
ax.text(
    5,
    6.3,
    "Does Phragmites + Liquidambar\nco-occur on a fault trace?",
    ha="center",
    va="center",
    fontsize=9,
    weight="bold",
    bbox=decision_style,
)

# Yes branch
ax.annotate(
    "", xy=(2.5, 5.5), xytext=(4, 5.9), arrowprops=dict(arrowstyle="->", lw=1.5)
)
ax.text(
    1.5, 5.7, "YES", ha="center", va="center", fontsize=9, weight="bold", color="green"
)
ax.text(
    2.5,
    5.0,
    "Zone A (Highest priority)\nSpring within 10 m\ndownslope of Phragmites",
    ha="center",
    va="center",
    fontsize=9,
    weight="bold",
    bbox=result_style,
)

# No branch
ax.annotate(
    "", xy=(7.5, 5.5), xytext=(6, 5.9), arrowprops=dict(arrowstyle="->", lw=1.5)
)
ax.text(
    8.5, 5.7, "NO", ha="center", va="center", fontsize=9, weight="bold", color="red"
)

# Secondary decision
ax.text(
    7.5,
    4.8,
    "Phragmites alone\non fault trace?",
    ha="center",
    va="center",
    fontsize=9,
    weight="bold",
    bbox=decision_style,
)

# Yes from secondary
ax.annotate(
    "", xy=(7.5, 4.0), xytext=(7.5, 4.4), arrowprops=dict(arrowstyle="->", lw=1.5)
)
ax.text(
    8.3, 4.2, "YES", ha="center", va="center", fontsize=8, weight="bold", color="green"
)
ax.text(
    7.5,
    3.3,
    "Zone B\nSpring within 20 m",
    ha="center",
    va="center",
    fontsize=9,
    weight="bold",
    bbox=result_style,
)

# No from secondary - go to third level
ax.annotate(
    "", xy=(9.5, 4.0), xytext=(8.5, 4.4), arrowprops=dict(arrowstyle="->", lw=1.5)
)
ax.text(
    10.2, 4.2, "NO", ha="center", va="center", fontsize=8, weight="bold", color="red"
)

ax.text(
    9.5,
    3.3,
    "Erica + Liquidambar\non fault trace?",
    ha="center",
    va="center",
    fontsize=9,
    weight="bold",
    bbox=decision_style,
)

# Yes from third
ax.annotate(
    "", xy=(9.5, 2.5), xytext=(9.5, 2.9), arrowprops=dict(arrowstyle="->", lw=1.5)
)
ax.text(
    10.3, 2.7, "YES", ha="center", va="center", fontsize=8, weight="bold", color="green"
)
ax.text(
    9.5,
    1.8,
    "Zone C (Seasonal)\nSpring within 30 m",
    ha="center",
    va="center",
    fontsize=9,
    weight="bold",
    bbox=result_style,
)

# No from third
ax.annotate(
    "", xy=(7.0, 2.5), xytext=(8.5, 2.9), arrowprops=dict(arrowstyle="->", lw=1.5)
)
ax.text(
    6.5, 2.7, "NO", ha="center", va="center", fontsize=8, weight="bold", color="red"
)
ax.text(
    7.0,
    1.8,
    "Zone D (Low priority)\nExcavate or shallow well\non fault trace with high-vigor Pinus",
    ha="center",
    va="center",
    fontsize=8,
    weight="bold",
    bbox=failure_style,
)

# Title
ax.text(
    5,
    11.8,
    "Workflow for Spring Prediction in Serpentinite Terrain\n(Marmaris Heuristic Framework)",
    ha="center",
    va="center",
    fontsize=12,
    weight="bold",
)

plt.tight_layout()
plt.savefig("spring_prediction_workflow.png", dpi=400, bbox_inches="tight")
plt.show()

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX


