# contact-app-using-tableview

viewcontroller.swift
struct Contact {
var name : String
var mobile : String
}

import UIKit

class ViewController: UIViewController {
    
    
    @IBOutlet weak var txtName: UITextField!
    
    @IBOutlet weak var txtMobile: UITextField!
    var contactArray : [Contact] = [Contact]()
    
    override func viewDidLoad() {
        super.viewDidLoad()
       
    }

    @IBAction func btnClear(_ sender: UIButton) {
        txtName.text = ""
        txtMobile.text = ""
    }
    
    @IBAction func btnSubmit(_ sender: UIButton) {
        
        let newContact = Contact(name: txtName.text!, mobile: txtMobile.text!)
        contactArray.append(newContact)
        for i in 0...contactArray.count-1{
            print(contactArray[i].name)
            print(contactArray[i].mobile)
        }
        txtName.text = ""
        txtMobile.text = ""
        
    }
    
    @IBAction func btnNext(_ sender: UIButton) {
        performSegue(withIdentifier: "next", sender: .none)
        
    }
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        if segue.identifier == "next"{
            let obj = segue.destination as! TableViewController
            obj.ctArray = contactArray
            
        }
    }
    

    
    }
    

dataviewcontroller.swift

import UIKit

class TableViewController: UITableViewController {
    
    var ctArray :[Contact] = [Contact]()
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
    }
    override func tableView(_ tableView:UITableView, numberOfRowsInSection section: Int) -> Int{return ctArray.count
    }
    
    
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath : IndexPath) -> UITableViewCell{
        let contact = ctArray[indexPath.row]
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell",for: indexPath) as! TableViewCell
        cell.lblName.text = contact.name
        cell.lblMobile.text = contact.mobile
        return cell
        
        
    }

}
 
 table viewcell
 
 import UIKit

class TableViewCell: UITableViewCell {

    @IBOutlet weak var lblName: UILabel!
    
    @IBOutlet weak var lblMobile: UILabel!
    
    override func awakeFromNib() {
        super.awakeFromNib()
        // Initialization code
    }

    override func setSelected(_ selected: Bool, animated: Bool) {
        super.setSelected(selected, animated: animated)

        // Configure the view for the selected state
    }

}
