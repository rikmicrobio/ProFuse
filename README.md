Here’s the updated `README.md` file with the names changed to `protein1.pdb` and `protein2.pdb`:

---

# ProFuse

**ProFuse** is a Python-based tool designed to fuse two protein structures by aligning the C-terminal of one protein to the N-terminal of another, creating a seamless chimeric protein. This is particularly useful for studying protein-protein interactions, chimeric protein design, and structural analysis.



![image_intoduction_ProFuse](https://github.com/user-attachments/assets/c98d74a3-089c-422f-9e3f-ab4d46db4a19)



## ✨ Features
- **Automated Protein Fusion**: ProFuse automatically aligns the C-terminal of the first protein to the N-terminal of the second, ensuring no overlap between the structures.
- **Flexible PDB Input**: Easily fuse any two PDB files representing protein structures.
- **Efficient and Fast**: Powered by the MDTraj library for rapid PDB file manipulation.
- **Colab-Ready**: The tool is optimized for Google Colab, allowing easy setup and use directly in your browser.
- **Downloadable Output**: After fusion, the combined protein structure is saved as a new PDB file and available for download.

## 🛠️ Installation

To use ProFuse, install the necessary dependencies using `pip`. The tool requires the MDTraj library, which you can install as follows:

```bash
!pip install mdtraj
```

## 🚀 Usage

To use **ProFuse**, upload your two PDB files to your environment (like Google Colab), and run the script. Here is an example of how to use the tool with two PDB files, `protein1.pdb` and `protein2.pdb`.

```python
import mdtraj as md
import numpy as np

# Load the PDB files
pdb1 = md.load('protein1.pdb')
pdb2 = md.load('protein2.pdb')

# Extract topologies and coordinates
top1, xyz1 = pdb1.top, pdb1.xyz
top2, xyz2 = pdb2.top, pdb2.xyz

# Get the C-terminal of pdb1 and N-terminal of pdb2
c_terminal_coords = xyz1[0, -1]
n_terminal_coords = xyz2[0, 0]

# Align N-terminal of pdb2 with C-terminal of pdb1
translation_vector = c_terminal_coords - n_terminal_coords
xyz2_translated = xyz2 + translation_vector

# Combine the structures
top_combined = top1.join(top2)
xyz_combined = np.concatenate((xyz1, xyz2_translated), axis=1)

# Save the fused structure
pdb_combined = md.Trajectory(xyz=xyz_combined, topology=top_combined)
pdb_combined.save('fused_protein.pdb')

# Download the result (if in Colab)
from google.colab import files
files.download('fused_protein.pdb')
```

### Example

When you run the script, it will:
1. Load two protein structures.
2. Align the second protein's N-terminal with the first protein's C-terminal.
3. Output a combined protein structure as `fused_protein.pdb`.

You can also run this tool directly on Google Colab using the link below:

[Run ProFuse on Google Colab](https://colab.research.google.com/drive/1VzHwXVOI-LYTKet1aHHRm36cmP6ifqTK#scrollTo=tkKhliFAPY_q)

## 📂 Example Files

Make sure to upload your PDB files before running the script. Here are two sample files you can use with the tool:

- `protein1.pdb`
- `protein2.pdb`

## 🔍 Visualizing the Result

You can visualize the fused protein structure using molecular visualization tools like [UCSF Chimera](https://www.cgl.ucsf.edu/chimera/) or [PyMOL](https://pymol.org/2/). Simply open the `fused_protein.pdb` file in one of these tools to examine the result.

## 🧬 Applications

- **Chimeric Protein Design**: Create fusion proteins by combining different domains or entire proteins.
- **Protein-Protein Interaction Studies**: Study potential interactions between fused domains.
- **Structural Analysis**: Analyze structural stability, flexibility, and interactions in chimeric proteins.

## 💡 Future Enhancements
- **Flexible Fusion Options**: Introduce options for different fusion points beyond N- and C-terminals.
- **Support for Multiple Proteins**: Allow fusion of more than two proteins in a single run.
- **Graphical Interface**: Develop a user-friendly graphical interface to simplify PDB file selection and fusion.

## 👨‍🔬 Contributors

- **Rik Ganguly** - Developer and creator of ProFuse.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Enjoy using **ProFuse** to seamlessly fuse your protein structures!

---

This `README.md` includes a description of the tool, instructions, and a link to the Colab notebook for easy execution.
