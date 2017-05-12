package notepad;

import java.awt.Dimension;
import java.awt.Toolkit;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;
import java.io.Reader;
import java.util.StringTokenizer;
import javax.swing.JFileChooser;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JTextPane;
import javax.swing.undo.CannotRedoException;
import javax.swing.undo.CannotUndoException;
import javax.swing.undo.UndoManager;

public class Actions {

	private String text = "";
	private String word = "";
	private String fileName = null;
	private int findIndex = -1;
	private JFileChooser jfc = new JFileChooser(".");
	private NoteFileFilter filter = new NoteFileFilter();
	Notepad n;
	public SetFont font = new SetFont();

	public Actions(Notepad n) {
		this.n = n;
	}

	public void newFile(JTextPane textPane, Notepad n) {
		n.textPane.setText("");
		fileName = null;
		n.setTitle("Untitled - JAVA Notepad SPL1");
	}

	public void open(JTextPane textPane, Notepad n) {
		int returnVal = jfc.showOpenDialog(n); // to show JFileChooser
		if (returnVal == JFileChooser.APPROVE_OPTION) {
			// to erase any text in the text area before adding new text
			n.textPane.setText(null);
			try {
				// to get the name of the selected file
				fileName = jfc.getSelectedFile().getPath();
				// to read the selected file
				Reader in = new FileReader(jfc.getSelectedFile());
				StringBuilder sb = new StringBuilder();
				// 100000 is the max. char can be written in the text area
				char[] buff = new char[100000];
				int nch;
				while ((nch = in.read(buff, 0, buff.length)) != -1) {
					sb.append(buff, 0, nch);
				}
				text = sb.toString();
				n.textPane.setText(text);
			} catch (FileNotFoundException x) {
				// no action
			} catch (IOException ioe) {
				System.err.println("I/O Error on Open");
			}
		}
		n.setTitle(jfc.getSelectedFile().getName() + " - JAVA Notepad");
	}

	public String save_as(JTextPane textPane) {

		String name = "";

		// filter the kind of files, we want only TXT file
		filter.addExtension("txt");
		// to set a description for the file (TXT)
		filter.setDescription("TXT Documents");
		// setting the FileFilter to JFileChooser
		jfc.setFileFilter(filter);
		int returnVal = jfc.showSaveDialog(textPane);
		if (returnVal == JFileChooser.APPROVE_OPTION) {
			// initializing the PrintWriter, to save the text in a new file
			PrintWriter fout = null;
			try {
				// Se existe extensão no arquivo
				if (jfc.getSelectedFile().toString().indexOf(".") != -1) {

					// Se o arquivo selecionado não tem a extensão txt, ele
					// adiciona
					if (jfc.getSelectedFile().toString().substring(
							jfc.getSelectedFile().toString().indexOf("."))
							.equals(".txt")) {

						fout = new PrintWriter(new FileWriter(jfc
								.getSelectedFile()));
						fileName = jfc.getSelectedFile().getPath();
					} else {
						fout = new PrintWriter(new FileWriter(jfc
								.getSelectedFile()
								+ ".txt"));
						fileName = jfc.getSelectedFile().getPath() + ".txt";
					}
				} else {
					fout = new PrintWriter(new FileWriter(jfc.getSelectedFile()
							+ ".txt"));
					fileName = jfc.getSelectedFile().getPath() + ".txt";
				}

				// getting the text from the text area
				text = textPane.getText();
				// getting the name of the selected file
				// fileName = jfc.getSelectedFile().getPath();
				// using StringTokenizer for the 'fileContent' String
				StringTokenizer st = new StringTokenizer(text, System
						.getProperty("line.separator"));
				while (st.hasMoreTokens()) {
					// write the string (text) in the selected file
					fout.println(st.nextToken());
				}
				// closing 'fout'
				fout.close();

				int i = fileName.lastIndexOf(".txt") - 1;
				int j = fileName.lastIndexOf('\\');
				do {
					System.out.println(fileName.charAt(i));
					name = fileName.charAt(i) + name;
					i--;
				} while (i > j);
			} catch (IOException ioe) {
				System.err.println("I/O Error on Save");
			}
		}
		return name;
	}

	public void save(JTextPane textPane) {
		if (fileName == null) {
			save_as(textPane);
		} else {
			// initializing 'fout' to write all text in the selected file
			PrintWriter fout = null;
			try {
				fout = new PrintWriter(new FileWriter(jfc.getSelectedFile()
						+ ".txt"));

				// for getting the text from the text area
				text = textPane.getText();
				// using StringTokenizer for the 'fileContent' String
				StringTokenizer st = new StringTokenizer(text, System
						.getProperty("line.separator"));
				while (st.hasMoreTokens()) {
					// write the string (text) in the selected file
					fout.println(st.nextToken());
				}
				// closing fout
				fout.close();
			} catch (IOException ioe) {
				System.err.println("I/O Error on Save");
			}
		}
	}

	public void exit(JTextPane textPane) {
		if (text.equals(textPane.getText())) {
			System.exit(0);
		} else {
			int option = JOptionPane.showConfirmDialog(null,
					"Do you want to save the changes?");

			if (option == 0) {
				save_as(textPane);
				System.exit(0);
			} else if (option == 1) {
				System.exit(0);
			}
		}
	}

	public void copy(JTextPane textPane) {
		textPane.copy();
	}

	public void cut(JTextPane textPane) {
		textPane.cut();
	}

	public void paste(JTextPane textPane) {
		textPane.paste();
	}

	public void select_all(JTextPane textPane) {
		textPane.selectAll();
	}

	public void find(JTextPane textPane) {
		word = JOptionPane.showInputDialog("Type the word to find");
		findIndex = textPane.getText().indexOf(word);

		if (findIndex == -1) {
			JOptionPane.showMessageDialog(null, "Word not found!", "No match",
					JOptionPane.WARNING_MESSAGE);
		} else {
			selectFound(textPane);
		}
	}

	public void find_next(JTextPane textPane) {
		int cont = 0;
		word = JOptionPane.showInputDialog("Type the word to find");
		findIndex = textPane.getText().indexOf(word);

		if (findIndex == -1) {
			JOptionPane.showMessageDialog(null, "Word not found!", "No match",
					JOptionPane.WARNING_MESSAGE);
		} else {
			while (findIndex < textPane.getText().length() && findIndex != -1) {
				selectFound(textPane);
				cont++;

				findIndex = findIndex + word.length();

				findIndex = textPane.getText().indexOf(word, findIndex);

				int response = JOptionPane.showConfirmDialog(null,
						"Find next match?", "FindNext",
						JOptionPane.YES_NO_OPTION, JOptionPane.PLAIN_MESSAGE,
						null);

				if (response == JOptionPane.NO_OPTION) {
					break;
				}
			}

			JOptionPane.showMessageDialog(null,
					"End of text! \nNumber of matches: " + cont);
		}
	}

	private void selectFound(JTextPane textPane) {
		textPane.grabFocus();
		textPane.select(findIndex, findIndex + word.length());
	}

	public void undo(UndoManager undo) {

		try {
			undo.undo();
		} catch (CannotUndoException ex) {
			System.out.println("Unable to undo: " + ex);
			Toolkit.getDefaultToolkit().beep();
		}

	}

	public void redo(UndoManager undo) {

		try {
			undo.redo();
		} catch (CannotRedoException ex) {
			System.out.println("Unable to redo: " + ex);
			Toolkit.getDefaultToolkit().beep();
		}

	}

	/**
	 *@see FONTS.JAVA this is a font class which is for changing the font,
	 *      style & size
	 */
	public void fonT(final JTextPane textPane) {
		font.setVisible(true); // setting the visible is true
		font.pack(); // pack the panel
		// making an action for ok button, so we can change the font
		font.getOkjb().addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent ae) {

				// n.getTextArea().setFont(font.font());
				textPane.setFont(font.font());

				// after we chose the font, then the JDialog will be closed
				font.setVisible(false);
			}
		});
		// making an action for cancel button, so we can return to the old font.
		font.getCajb().addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent ae) {
				// after we cancel the, then the JDialog will be closed
				font.setVisible(false);
			}
		});
	}

	public void about() {

		JFrame frame = new JFrame();
		JLabel label = new JLabel(
				"<html><b>Notepad Software Product Line<BR></b>"
						+ "Versão 1.0 - 2012</html>");

		frame.setTitle("About Notepad SPL");
		frame.setSize(250, 125);
		frame.setResizable(false);

		Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();
		frame.setLocation((screenSize.width - frame.getWidth()) / 2,
				(screenSize.height - frame.getHeight()) / 2);

		frame.add(label);
		frame.setVisible(true);
	}
}
