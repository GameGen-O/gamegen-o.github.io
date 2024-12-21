The previous repo has expired, now re-upload.

# About GameGen-O
We introduce GameGen-O, the first diffusion transformer model specifically designed for both generating and interactively controlling open-world game videos. This model facilitates high-quality, open-domain generation by simulating an extensive array of game engine features, such as innovative characters, dynamic environments, complex actions, and diverse events. Additionally, it provides interactive controllability, predicting and altering future content based on the current clip, thus allowing for gameplay simulation. To realize this vision, we first collected and built an Open-World Video Game Dataset (OGameData) from scratch. It is the first and largest dataset for open-world game video generation and control, which comprises over one million diverse gameplay video clips with informative captions from GPT-4o. GameGen-O undergoes a two-stage training process, consisting of pre-training and instruction tuning. Firstly, the model was pre-trained via text-to-video generation and video continuation, endowing it with the capability for long-sequence, high-quality open-domain game video generation. Further, to achieve interactive controllability, we designed InstructNet to incorporate game-related multi-modal control signal experts. This allows the model to adjust latent representations based on user inputs, unifying character interaction, and scene content control for the first time in video generation. During instruction tuning, only the InstructNet is updated while the pre-trained foundation model is frozen, enabling the integration of interactive controllability without loss of diversity and quality of generated content. GameGen-O represents a significant leap forward in open-world game design using generative models. It demonstrates the potential of generative models to serve as auxiliary tools to traditional rendering techniques, effectively merging creative generation with interactive capabilities. The project will be available at ([[https://gamegen-o.github.io/](https://github.com/GameGen-O/gamegen-o.github.io)]([https://gamegen-o.github.io](https://github.com/GameGen-O/gamegen-o.github.io)))

# Author Update 20241220
We have observed the recent endeavors by Swarms in the Crypto domain and were inspired to explore a creative intersection between their work and our own. Leveraging the capabilities of GameGen-O, we embarked on generating a meme image that captures the quintessential Crypto aesthetic. The result is a charming depiction of a Shiba Inu, a beloved figure in meme culture, meticulously crafted in the distinctive style of our model. We have affectionately named this creation **GenO**.

GenO not only showcases the versatility and artistic prowess of GameGen-O but also embodies our aspirations for continuous model optimization. By integrating the playful and vibrant elements characteristic of Crypto-themed memes, GenO serves as a symbolic representation of our commitment to innovation and excellence. Moreover, it acts as a beacon of hope and motivation, encapsulating our desire for our research to gain recognition within the academic community. We fervently hope that GenO will bring good fortune and positive energy to our endeavors, ultimately contributing to our paper's success in securing the prestigious Best Paper award.

Through the creation of GenO, we aim to bridge the gap between cutting-edge generative models and popular cultural trends, demonstrating the potential of GameGen-O to produce engaging and relevant content. This initiative not only highlights the practical applications of our model but also underscores our dedication to pushing the boundaries of what generative technology can achieve in both creative and interactive domains.

![1734744423594](https://github.com/user-attachments/assets/74646538-d30a-44ee-84a4-ba99c86f1e85)

# OGameData

## Data Availability Statement
We are committed to maintaining transparency and compliance in our data collection and sharing methods. Please note the following:

- **Publicly Available Data**: The data utilized in our studies is publicly available. We do not use any exclusive or private data sources.

- **Data Sharing Policy**: Our data sharing policy aligns with precedents set by prior works, such as [InternVid](https://github.com/OpenGVLab/InternVideo/tree/main/Data/InternVid), [Panda-70M](https://snap-research.github.io/Panda-70M/) 
, and [Miradata](https://github.com/mira-space/MiraData). Rather than providing the original raw data, we only supply the YouTube video IDs necessary for downloading the respective content.

- **Usage Rights**: The data released is intended exclusively for research purposes. Any potential commercial usage is not sanctioned under this agreement.

- **Compliance with YouTube Policies**: Our data collection and release practices strictly adhere to YouTube’s data privacy policies and fair of use policies. We ensure that no user data or privacy rights are violated during the process.

- **Data License**: The dataset is made available under the Creative Commons Attribution 4.0 International License (CC BY 4.0).

## Clarifications

- The OGameData dataset is only available for informational purposes only. The copyright remains with the original owners of the video.
- All videos of the OGameData dataset are obtained from the Internet which is not the property of our institutions. Our institution is not responsible for the content or the meaning of these videos.
- You agree not to reproduce, duplicate, copy, sell, trade, resell, or exploit for any commercial purposes, any portion of the videos, and any portion of derived data. You agree not to further copy, publish, or distribute any portion of the OGameData dataset.

## Datadaset Construction Pipeline
### Data Collection and Filtering
- **Sources**: Content was gathered from internet gameplay videos, focusing on gameplay footage with minimal UI elements.
- **Manual Filtering**: Low-quality videos were manually filtered out, ensuring the integrity of metadata such as game name, genre, and player perspective.

### Data Processing Pipeline
- **Scene Segmentation**: Videos were segmented into 16-second clips using PyScene and TransNetV2, discarding clips shorter than 4 seconds.
- **Aesthetic Scoring**: Clips were scored using CLIP-AVA for aesthetic quality.
- **Motion Filtering**: UniMatch was used to filter clips based on motion.
- **Content Similarity**: VideoCLIP was employed to ensure content diversity.
- **Camera Motion Annotation**: CoTrackerV2 annotated clips with camera motion information.

![Pipeline](https://arxiv.org/html/2411.00769v1/x2.png)

## Dataset Overview
### OGameData
The `OGameData` dataset consists of 1,000,000 video samples curated from online gaming content. Each data sample includes metadata on video paths, text descriptions, captions, timestamps, and source URLs. Three smaller datasets, containing 10K, 50K, and 100K samples respectively, are available for quick testing and experimentation.

### File Descriptions
- **`OGameData.csv`**: The full dataset, under review and coming soon.
- **`OGameData_250K.csv`**: A compact subset of 250,000 generation training samples, ideal for initial experimentation.
- **`OGameData_100K.csv`**: A subset of `OGameData` containing 100,000 generation training samples.
- **`OGameData_50K.csv`**: A smaller subset containing 50,000 generation training samples.

### Data Fields
Each `.csv` file contains the following columns:
- **filename**: The video filename, derived from the original video ID and corresponding splitting ID, with a format such as `VIDEOID_scene-SPLITINGID.mp4`.
- **text**: Descriptive text accompanying each video clip with structural annotations.
- **short_caption**: A brief caption summarizing each video clip.
- **start_time**: The start time of the video segment in seconds.
- **end_time**: The end time of the video segment in seconds.
- **URL**: The source URL for each video, linking to the original content.

### Example Data Entry
| Text | Short Caption | Start Time | End Time | URL | Filename |
|------|---------------|------------|----------|-----|----------|
| "Player achieves a new high score by defeating a boss" | "Player defeats boss" | 00:02:15 | 00:02:30 | `https://www.youtube.com/watch?v=video1` | `video1.mp4` |

### Download Links
- **[OGameData_250K.csv](https://drive.google.com/file/d/1hd3aiGBiDClQMSqFZCheysg1K2zLPSm4/view?usp=drive_link)** (250,000 samples)
- **[OGameData_100K.csv](https://drive.google.com/file/d/1O80GdWI4BfhwWIIvEyoGZmBrK_NZae2k/view?usp=sharing)** (100,000 samples)
- **[OGameData_50K.csv](https://drive.google.com/file/d/1Zw4AofuVso53RCmNtx5GNN3MdFxhvg2H/view?usp=sharing)** (50,000 samples)

## License
The `OGameData` dataset is available under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). Please ensure proper attribution when using the dataset in research or other projects.

## Acknowledgement

Our dataset construction pipeline is inspired by and leverages the following repositories and resources:

- **[LAION-400 Open Dataset](https://laion.ai/blog/laion-400-open-dataset/)**
- **[InternVid](https://github.com/OpenGVLab/InternVideo/tree/main/Data/InternVid)**
- **[OpenVid-1M](https://github.com/NJU-PCALab/OpenVid-1M)**
- **[HD-VG-130M](https://github.com/daooshee/HD-VG-130M)**
- **[Vript](https://github.com/mutonix/Vript)**
- **[MiraData](https://github.com/mira-space/MiraData)**
- **[Panda-70M](https://snap-research.github.io/Panda-70M/)**
- **[OpenSora](https://github.com/hpcaitech/Open-Sora)**
- **[OpenSora-Plan](https://github.com/PKU-YuanGroup/Open-Sora-Plan)**

We extend our gratitude to the authors and contributors of these resources for their invaluable work and contributions to the field.

---

## Citation
If you use `OGameData` in your research, please cite it as follows:

```markdown
@article{che2024gamegen,
  title={GameGen-O: Interactive Open-world Game Video Generation},
  author={Che, Haoxuan and He, Xuanhua and Liu, Quande and Jin, Cheng and Chen, Hao},
  journal={arXiv preprint arXiv:2411.00769},
  year={2024}
}
```

## Contact

For questions, please open an issue on our [GitHub repository](https://github.com/GameGen-O/) or reach out via our contact page.
