package notepad;


import java.awt.Container;
import java.awt.Dimension;
import java.awt.Toolkit;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JFrame;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JMenuItem;
import javax.swing.JScrollPane;
import javax.swing.JTextPane;
import javax.swing.event.UndoableEditEvent;
import javax.swing.event.UndoableEditListener;
import javax.swing.text.JTextComponent;
import javax.swing.undo.UndoManager;


public class Notepad extends JFrame implements ActionListener {

	private static final long serialVersionUID = 1L;
	public JTextPane textPane;
	private JMenuBar menuBar = new JMenuBar();
	public JMenu file = new JMenu("File");
	private JMenu edit = new JMenu("Edit");
	private JMenu format = new JMenu("Format");
	private JMenu help = new JMenu("Help");

	public Actions actions = new Actions(this);
	
	//for using undo & redo
	public UndoManager undo = new UndoManager();

	public static void main(String[] args) {
		new Notepad().setVisible(true);
	}

	public Notepad() {
		super();
		{
			{
				setTitle("Untitled - JAVA Notepad SPL1");
				setSize(800, 600);
				this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
				
				Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();
				this.setLocation((screenSize.width-this.getWidth())/2,(screenSize.height-this.getHeight())/2);
			}
			{
				Container container = getContentPane();
				textPane = new JTextPane();
				container.add(textPane);
				container.add(new JScrollPane(textPane));

				this.montaMenu();
			}
			{
				getTextComponent().getDocument().addUndoableEditListener( new UndoableEditListener() {
					public void undoableEditHappened( UndoableEditEvent e ) {
						//Remember the edit and update the menus
						undo.addEdit( e.getEdit() );
						//undoAction.update();
						//redoAction.update();
					}
				} );
			}
		}
	}

	public void montaMenu() {

		//Menu File
		JMenuItem itemNew = new JMenuItem("New");
		itemNew.addActionListener(this);
		JMenuItem itemOpen = new JMenuItem("Open...");
		itemOpen.addActionListener(this);
		JMenuItem itemPrint = new JMenuItem("Print");
		itemPrint.addActionListener(this);
		JMenuItem itemSave = new JMenuItem("Save");
		itemSave.addActionListener(this);
		JMenuItem itemSave_As = new JMenuItem("Save As");
		itemSave_As.addActionListener(this);
		JMenuItem itemExit = new JMenuItem("Exit");
		itemExit.addActionListener(this);

		file.add(itemNew);
		file.add(itemOpen);
		file.addSeparator();
		file.add(itemPrint);
		file.addSeparator();
		file.add(itemSave);
		file.add(itemSave_As);
		file.addSeparator();
		file.add(itemExit);

		// Menu Edit
		JMenuItem itemCopy = new JMenuItem("Copy");
		itemCopy.addActionListener(this);
		JMenuItem itemCut = new JMenuItem("Cut");
		itemCut.addActionListener(this);
		JMenuItem itemPaste = new JMenuItem("Paste");
		itemPaste.addActionListener(this);
		JMenuItem itemSelect_All = new JMenuItem("Select All");
		itemSelect_All.addActionListener(this);
		JMenuItem itemFind = new JMenuItem("Find");
		itemFind.addActionListener(this);
		JMenuItem itemFind_Next = new JMenuItem("Find Next");
		itemFind_Next.addActionListener(this);
		JMenuItem itemRedo = new JMenuItem("Redo");
		itemRedo.addActionListener(this);
		JMenuItem itemUndo = new JMenuItem("Undo");
		itemUndo.addActionListener(this);

		edit.add(itemCopy);
		edit.add(itemCut);
		edit.add(itemPaste);
		edit.addSeparator();
		edit.add(itemSelect_All);
		edit.addSeparator();
		edit.add(itemFind);
		edit.add(itemFind_Next);
		edit.addSeparator();
		edit.add(itemRedo);
		edit.add(itemUndo);

		// Menu Format
		JMenuItem itemSet_Font = new JMenuItem("Set Font");
		itemSet_Font.addActionListener(this);
		JMenuItem itemLine_Wrap = new JMenuItem("Line Wrap");
		itemLine_Wrap.addActionListener(this);

		format.add(itemSet_Font);
		format.add(itemLine_Wrap);

		// Menu Help
		JMenuItem itemAbout = new JMenuItem("About");
		itemAbout.addActionListener(this);

		help.add(itemAbout);

		menuBar.add(file);
		menuBar.add(edit);
		menuBar.add(format);
		menuBar.add(help);

		setJMenuBar(menuBar);
	}

	public void actionPerformed(ActionEvent evt) {
		if (evt.getActionCommand().equals("New")) {
			actions.newFile(textPane, this);
		} else if (evt.getActionCommand().equals("Open...")) {
			actions.open(textPane, this);
		} else if (evt.getActionCommand().equals("Print")) {
			System.out.println("Print");
		} else if (evt.getActionCommand().equals("Save")) {
			actions.save(textPane);
		} else if (evt.getActionCommand().equals("Save As")) {
			String fileName = actions.save_as(textPane);
			setTitle(fileName+" - JAVA Notepad SPL1");
		} else if (evt.getActionCommand().equals("Exit")) {
			actions.exit(textPane);
		} else if (evt.getActionCommand().equals("Copy")) {
			actions.copy(textPane);
		} else if (evt.getActionCommand().equals("Cut")) {
			actions.cut(textPane);
		} else if (evt.getActionCommand().equals("Paste")) {
			actions.paste(textPane);
		} else if (evt.getActionCommand().equals("Select All")) {
			actions.select_all(textPane);
		} else if (evt.getActionCommand().equals("Find")) {
			actions.find(textPane);
		} else if (evt.getActionCommand().equals("Find Next")) {
			actions.find_next(textPane);
		} else if (evt.getActionCommand().equals("Redo")) {
			actions.redo(undo);
		} else if (evt.getActionCommand().equals("Undo")) {
			actions.undo(undo);
		} else if (evt.getActionCommand().equals("Set Font")) {
			actions.fonT(textPane);
		} else if (evt.getActionCommand().equals("Line Wrap")) {
			//actions.lineWrap(textPane);
		} else if (evt.getActionCommand().equals("About")) {
			actions.about();
		}
	}
	
	public JTextComponent getTextComponent() {
		return textPane;
	}
}
