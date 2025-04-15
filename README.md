import cv2
import numpy as np

# Ruta a tu imagen térmica.  Recuerda reemplazar esto con la ruta correcta.
image_path = './imagen/termica.jpg'

try:
    # Lee la imagen en escala de grises
    img = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)

    # Verifica si la imagen se cargó correctamente
    if img is None:
        raise FileNotFoundError(f"Error: No se pudo cargar la imagen desde {image_path}")

    # Normaliza la imagen para obtener mejores resultados con el colormap
    img_normalized = cv2.normalize(img, None, 0, 255, cv2.NORM_MINMAX, cv2.CV_8U)


    # Aplica diferentes colormaps
    colormap_jet = cv2.applyColorMap(img_normalized, cv2.COLORMAP_JET)
    colormap_viridis = cv2.applyColorMap(img_normalized, cv2.COLORMAP_VIRIDIS)
    colormap_plasma = cv2.applyColorMap(img_normalized, cv2.COLORMAP_PLASMA)
    colormap_magma = cv2.applyColorMap(img_normalized, cv2.COLORMAP_MAGMA)
    colormap_inferno = cv2.applyColorMap(img_normalized, cv2.COLORMAP_INFERNO)


    # Mostrar y guardar las imágenes
    cv2.imshow('Original', img)
    cv2.imshow('Jet', colormap_jet)
    cv2.imshow('Viridis', colormap_viridis)
    cv2.imshow('Plasma', colormap_plasma)
    cv2.imshow('Magma', colormap_magma)
    cv2.imshow('Inferno', colormap_inferno)

    cv2.imwrite('thermal_jet.png', colormap_jet)
    cv2.imwrite('thermal_viridis.png', colormap_viridis)
    cv2.imwrite('thermal_plasma.png', colormap_plasma)
    cv2.imwrite('thermal_magma.png', colormap_magma)
    cv2.imwrite('thermal_inferno.png', colormap_inferno)

    cv2.waitKey(0)
    cv2.destroyAllWindows()

except FileNotFoundError as e:
    print(e)  # Imprime el mensaje de error más detallado
except Exception as e:
    print(f"Ocurrió un error inesperado: {e}") #Maneja otros errores posibles


