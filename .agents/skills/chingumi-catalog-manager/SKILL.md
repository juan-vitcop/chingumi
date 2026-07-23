---
name: chingumi-catalog-manager
description: Manage the Chingumi product catalog, update prices/stock, handle product images, and keep both the PDF catalog and the web repository in sync.
---

# Skill: Chingumi Product Catalog & Price List Manager

## Overview
This skill outlines the standard operating procedure for managing the Chingumi product catalog, updating prices/stock, handling product images, and keeping both the PDF catalog and the web repository in sync.

---

## 1. Catalog Standards & Formatting
- **Target Sheets**: Primarily **Lista Mayorista** (unless specified otherwise, e.g., Lista Minorista, Vieja, Lista para web).
- **Column Structure**:
  - `PRODUCTO`: Standardized product name in uppercase, including brand and origin if applicable (e.g., `RAMEN SHIN CUP - ORIGEN COREANO`).
  - `PRESENTACIÓN`: Quantity, volume, weight, or unit packaging (e.g., `68 GR`, `500 ML`, `1 KG`, `CAJA X 20 UNIDADES`).
  - `IMAGEN`: Image reference / URL / identifier.
  - `PRECIO`: Price formatted as currency (e.g., `$7.900`) or status flags (e.g., `SIN STOCK`).
- **Multiple Sizes / Variants**: For products with multiple sizes, combine them into a single line in the output summary table, separated by a slash `/` (e.g., `LECHE DE COCO SUREE - COCONUT MILK` | `165 ML / 400 ML` | `$2.800 / $4.800`).
- **Retail Pricing (Minorista)**: When calculating retail prices, add a 30% markup to the wholesale (mayorista) price, always rounding the final amount to a number that ends in 0 (e.g., `$3.600` mayorista × 1.30 = `$4.680` minorista).

---

## 2. Image Processing Requirements
When the user uploads a photo for a new product:
1. **Background Removal**: Ensure/verify that the image has a transparent or pure white background, matching existing product photo standards.
2. **Local Storage**: Save/download the processed image directly to the local folder:
   `/Users/juanignaciovitcop/Documents/Chingumi/chingumi fotos/`
3. **Naming Convention**: Use a clear, kebab-case or standardized naming matching the product title (e.g., `ramen-shin-cup.png`).

---

## 3. Workflow Execution Steps

### Step A: Update Data & Generate Deliverables
1. Apply requested modifications (Add, Edit, Delete, or Set "SIN STOCK").
2. Format naming and presentation consistently with existing entries.
3. Generate the updated **PDF Document** ready for distribution via WhatsApp/Print.

### Step B: Output Summary Table for Web LLM Sync
Every update must conclude with a markdown summary table so the user can easily copy/paste it into their code editor LLM to update the web repo.

**Table Format Example**:
| Accion | Producto | Presentacion | Precio / Estado | Archivo Imagen Local |
| :--- | :--- | :--- | :--- | :--- |
| **Agregar** | RAMEN SHIN CUP - ORIGEN COREANO | 68 GR | $3.100 | `/Users/juanignaciovitcop/Documents/Chingumi/chingumi fotos/ramen-shin-cup.png` |
| **Actualizar** | BEBIDAS OKF SABORIZADAS | 350 ML | $3.100 | - |
| **Sin Stock** | PASTA MISO ORIGINAL | 140 GR | SIN STOCK | - |
| **Eliminar** | PRODUCTO X | 100 GR | - | - |

---

## 4. Response Protocol
Whenever a user asks to update prices, stock, or add/remove products:
1. Confirm the changes made.
2. Provide the generated PDF file.
3. Display the Markdown Summary Table for the editor LLM integration.
