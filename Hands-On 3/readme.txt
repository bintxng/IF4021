--Tugas Hands-On 3--
Rekamlah sebuah video yang berdurasi kira-kira 60 detik dengan kamera ponsel. Toleransi durasi adalah 63 detik.
Resolusi video haruslah tepat 1920x1080 dengan FPS 30.
Pindahkan catatan tersebut ke dalam csv dengan format sebagai berikut:
| Nafas-ke | Second | Milisecond |
|----------|--------|-----------|
| 1        | 0      | 0         |
| 2        | 10     | 0         |

Membuat video dari gambar (image sequence)
Definisikan lokasi direktori dari gambar yang akan dijadikan video.

IMGS_PATH = (os.path.join(os.getcwd(), 'data', 'toby-rgb'))
list_imgs = glob(IMGS_PATH + '/*.jpg')
print(f"5 path pertama: {list_imgs[:5]}")

Jangan lupa, jika bekerja dengan image sequence, pastikan urutan nama file sudah sesuai. Bila perlu, lakukan sorting
list_imgs = sorted(list_imgs, key=lambda x: int(x.split('/')[-1].split('.')[0]))
print(f"5 path pertama setelah diurutkan: {list_imgs[:5]}")
print(f"Total jumlah gambar: {len(list_imgs)}")

Soal 1.
Jelaskan maksud dari list_imgs = sorted(list_imgs, key=lambda x: int(x.split('/')[-1].split('.')[0]))
------------------------------------------------------------------------------------------------------
Memuat semua gambar yang ada di dalam list_imgs ke dalam numpy array. Setiap gambar akan diubah menjadi array 3 dimensi (RGB).
images = []
for img_path in list_imgs:
    img = cv2.imread(img_path)
    images.append(img)

images_array = np.array(images)

print(f"Shape of images_array: {images_array.shape}")

Shape of images_array: (1800, 1080, 1920, 3)
Dapat kita amati bahwa ukuran dari images_array adalah berformat (jumlah gambar, tinggi, lebar, channel) atau umumnya ditulis (t, h, w, c)

Sekarang, mari kita buat sebuah video dari image sequence yang telah kita muat ke dalam images_array.
Warning! Mungkin komputer Anda akan kehabisan memori jika jumlah gambar yang dijadikan video terlalu banyak. Jika hal ini terjadi, Anda bisa mengurangi jumlah gambar yang dijadikan video atau menggunakan komputer dengan spesifikasi yang lebih tinggi.

save_loc = os.path.join(os.getcwd(), 'data', 'toby-rgb.mp4')
fourcc = cv2.VideoWriter_fourcc(*'mp4v')
height, width, layers = images_array[0].shape
video = cv2.VideoWriter(save_loc, fourcc, 30, (width, height))

for image in images_array:
    video.write(image)

video.release()

Soal 2.
fourcc = cv2.VideoWriter_fourcc(*'mp4v')
Apakah ada opsi lain selain mp4v? Jika ada, coba gunakan dan jelaskan.

